---
title: Devise to Sorcery
date: 2024-08-22 12:00:00 -0700
tags: software
header:
  image: /assets/images/posts/2024-08-23-header.jpg
  teaser: /assets/images/posts/2024-08-23-header.jpg
---

This article describes the process of migrating a Ruby on Rails app from [Devise](https://github.com/heartcombo/devise) to [Sorcery](https://github.com/Sorcery/sorcery)  authentication gems. The related pull requests can be viewed on GitHub:

* [jcraigk/phishin - Sorcery #383](https://github.com/jcraigk/phishin/pull/383)
* [jcraigk/phishin - Remove Devise user columns #385](https://github.com/jcraigk/phishin/pull/385)


## Authentication in Rails

The Rails ecosystem has several good options for handling user authentication, which covers interactions like signing up, logging in, resetting a password, etc. One of the earliest and most popular of these is [Devise](https://github.com/heartcombo/devise), originally written by José Valim who would later create the [Elixir](https://elixir-lang.org/) programming language. Devise is a Rails engine, an [omakase](https://en.wikipedia.org/wiki/Omakase) all-in-one solution that provides a minimal footprint in an app's visible code while providing all the necessary pieces - model, view, and controller logic - behind the scenes. Using Devise is often the best way to get an app up and running quickly.

As apps grow, custom business logic eventually crops up around authentication features and that logic needs to jibe with the auth library we've chosen. Because Devise brings all the pieces for us, it becomes a game of overriding controller actions, model methods, and view templates when we need to add custom logic. It can be messy and burdensome to maintain these overrides, which often do not follow the local naming and style conventions of our app.

An alternative approach is to pick a library that supplies the core authentication features we need and implement the controller and view logic ourselves. This is the way of the [Sorcery](https://github.com/Sorcery/sorcery) gem. Although this means more work for the developer upfront, in the longterm having the relevant code exposed and expressed in our app's local convention is a boon to longterm maintainability.

Sorcery’s name is somewhat ironic in that it actually dispels the “magic” that happens behind the scenes when using a Rails engine like Devise.


## Our Goals

Let's walk through the process of migrating an existing Rails app from Devise to Sorcery. We have three goals:

  * Maintain existing users and passwords
  * Allow for fast rollback if something goes wrong in production
  * Add Google [OAuth](https://oauth.net/2/)-based logins


## Database Migrations

First, we need to take our existing `users` table and add the columns Sorcery needs for the features we've chosen. In this app we are using the  `remember_me` and `reset_password` modules. We'll be adding the `external` module for Google OAuth logins as well. The individual migrations for each module can be generated separately by the Sorcery gem, but below we will combine them:

```ruby
# db/migrate/..._install_sorcery.rb

class InstallSorcery < ActiveRecord::Migration[7.2]
  def change
    add_column :users, :crypted_password, :string
    execute "UPDATE users SET crypted_password = encrypted_password"
    add_column :users, :salt, :string

    add_column :users, :reset_password_token_expires_at, :datetime, default: nil
    add_column :users, :reset_password_email_sent_at, :datetime, default: nil
    add_column :users, :access_count_to_reset_password_page, :integer, default: 0

    add_column :users, :remember_me_token, :string, default: nil
    add_column :users, :remember_me_token_expires_at, :datetime, default: nil
    add_index :users, :remember_me_token

    create_table :authentications do |t|
      t.references :user
      t.string :provider, :uid, null: false
      t.timestamps null: false
    end

    add_index :authentications, %i[provider uid]
  end
end
```

To satisfy our requirement of fast rollbacks, we keep all of the existing Devise columns and duplicate the contents of `encrypted_password` to Sorcery's differently named `crypted_password`. Luckily, both gems use `bcrypt` so passwords will not have to be reset after deploying the changes. Note that Sorcery uses a `salt` column to improve password security but handles the absence of salt gracefully for existing users.

We can deploy the following cleanup migration to production after a grace period to ensure we don't need to roll back to Devise:

```ruby
class RemoveDeviseCols < ActiveRecord::Migration[7.2]
  def change
    remove_column :users, :encrypted_password, :datetime
    remove_column :users, :reset_password_sent_at, :datetime
    remove_column :users, :remember_created_at, :datetime
    remove_column :users, :sign_in_count, :integer
    remove_column :users, :current_sign_in_at, :datetime
    remove_column :users, :last_sign_in_at, :datetime
    remove_column :users, :current_sign_in_ip, :inet
    remove_column :users, :last_sign_in_ip, :inet
    remove_column :users, :confirmation_token, :string
    remove_column :users, :confirmed_at, :datetime
    remove_column :users, :confirmation_sent_at, :datetime
    remove_column :users, :unconfirmed_email, :string
    remove_column :users, :authentication_token, :string
  end
end
```

## The User Model

I like to use [Rails concerns](https://api.rubyonrails.org/v7.1.3.4/classes/ActiveSupport/Concern.html) for grouping business logic in the model hierarchy. The authentication features we're adding seem like a good candidate for this pattern. Let's create a concern:

```ruby
# app/models/concerns/sorcery_authenticable.rb

module SorceryAuthenticable
  extend ActiveSupport::Concern

  included do
    authenticates_with_sorcery!

    has_many :authentications, dependent: :destroy

    validates :username, presence: true, uniqueness: true,
    validates :email, uniqueness: true, format: { with: URI::MailTo::EMAIL_REGEXP }
    validates :password, length: { minimum: 5 }, if: :password
    validates :password, confirmation: true, if: :password

    before_save :assign_username_from_email

    private

    def assign_username_from_email
      return if username.present?

      name = email.split("@").first.gsub(/[^A-Za-z0-9_]/, "_")
      name = "#{name.first(10)}_#{SecureRandom.hex(2)}" if User.where(username: name).exists?
      self.username = name
    end
  end
end

```

Note the logic in `assign_username_from_email` for creating usernames from email addresses in the case of OAuth signups. Not all apps will have the `username` column, but this app happens to rely on it for user identification and sharing, so we need a unique username for each user.

The `authenticates_with_sorcery!` call provides our model with the methods we'll need during runtime, such as `valid_password?`

Now we simply include the concern in our `User` model:

```ruby
class User < ApplicationRecord
  include SorceryAuthenticable
end
```


## Routes

Instead of a single call in the `config/routes.rb` file like Devise's `devise_for` method, we must define our own routes:

```ruby
  namespace :oauth do
    get "callback/:provider", to: "sorcery#callback"
    get ":provider", to: "sorcery#oauth", as: :at_provider
  end
  resources :users, only: %i[new create]
  resources :user_sessions, only: %i[new create destroy]
  resources :password_resets, only: %i[new create edit update]
  get "login", to: "user_sessions#new", as: :login
  delete "logout", to: "user_sessions#destroy", as: :logout
```

We begin with our OAuth routes for external provider logins, then define our resources which include users, sessions, and password resets. We also define a couple of convenience methods so we can use `login_path` and `logout_path` in our controller.


## Controllers

Now we get to implement our controller logic using Sorcery's core methods (`login`, `logout`, `current_user`, etc). We'll end up with four controllers:

```
app/controllers/oauth/sorcery_controller.rb
app/controllers/password_resets_controller.rb
app/controllers/user_sessions_controller.rb
app/controllers/users_controller.rb
```

We won't go over all of the code, which can be  [viewed on GitHub](https://github.com/jcraigk/phishin/pull/383/files), but here is a snippet showing the logic that handles logging in and out:

```ruby
# app/controllers/user_sessions_controller.rb

class UserSessionsController < ApplicationController
  def new
    return redirect_to root_path if current_user
    @user = User.new
  end

  def create
    if valid_credentials?
      auto_login(@user, true)
      redirect_back_or_to root_path, notice: t("auth.login_success")
    else
      redirect_to new_user_session_path, alert: t("auth.login_fail")
    end
  end

  def destroy
    logout
    redirect_to login_path, notice: t("auth.logout_success")
  end

  private

  def valid_credentials?
    @user = User.find_by(email: params[:email])
    @user&.valid_password?(params[:password])
  end
end
```

Note the calls to Sorcery's `current_user`, `auto_login`, `valid_password?`, and `logout` methods.


## Views

To accommodate the controller actions we've added, we'll next add the corresponding views. We'll end up with something like this:

```
app/views/password_resets/edit.html.slim
app/views/password_resets/new.html.slim
app/views/user_mailer/reset_password.text.erb
app/views/user_sessions/new.html.slim
app/views/users/new.html.slim
```

This app happens to use [Slim](https://github.com/slim-template/slim) for its HTML templating, but we would subtitute `.erb` for `.slim` if our app uses the more conventional ERB (as we do for the password reset mail template).

Here's a snippet from the login page:

```slim
/ app/views/user_sessions/new.html.slim

= render partial: "layouts/global_nav"

#content_box
  h1 = t("auth.login_provider")
  = render "shared/external_login_buttons"

  h1 = t("auth.login_email")
  = form_with url: user_sessions_path, method: :post, local: true do |f|

    .field_label = t("auth.email")
    .field_content = f.email_field :email, autofocus: true

    .field_label = t("auth.password")
    .field_content = f.password_field :password

    .field_label = submit_button(t("auth.login"))

  .instructions
    = link_to t("auth.signup"), new_user_path
    = link_to t("auth.reset_password"), new_password_reset_path
```

One last note: instead of Devise's `user_signed_in?` method, we'll need to use Sorcery's shorter `logged_in?`. We can accomplish this with a global search and replace in our text editor.


## OAuth

In order to add a Google OAuth-based login option to the site, we need to first create an app using Google Cloud Services, and configure its OAuth consent screen. To adhere to Google's requirements, we must add a Privacy Policy and Terms of Service to our site. These can be simple statements but they must exist or Google will reject the app.

Once the app is setup in the Cloud console, Google gives us the necessary credentials, which we'll store in environment variables `OAUTH_GOOGLE_KEY` and `OAUTH_GOOGLE_SECRET`.

We can now add our "Sign In with Google" button. The following partial is built to handle multiple OAuth providers, which we'll take advantage of at a later time when we expand login options.

```slim
/ app/views/shared/_external_login_buttons.html.slim

.external-login-container
  - App.oauth_providers.each do |provider|
    = link_to oauth_at_provider_path(provider:),
              class: "button external-login-btn #{provider}-btn non-remote" do
      .login-logo = image_pack_tag "static/images/external-logos/#{provider}.png", alt: "#{provider.to_s.titleize} Logo", size: "18x18"
      = t("auth.#{provider}_login")
```

Adding the necessary logo image and CSS completes the job.


## Tests

Most of our tests around users and authentication will remain the same during the migration process and will serve as confidence builders as we make changes. One notable change is that we need to create our own `sign_in` method to replace the old `login_as`:

```ruby
# spec/support/sorcery.rb

RSpec.configure do |config|
  config.include Sorcery::TestHelpers::Rails
end

module Sorcery
  module TestHelpers
    module Rails
      def sign_in(user)
        visit login_path
        fill_in "email", with: user.email
        fill_in "password", with: "password"
        click_on I18n.t("auth.login")
      end
    end
  end
end
```

## No Gem is Perfect

One drawback of Sorcery is that it doesn't expose an option to merge OAuth based authentications with existing users who may have signed up earlier. For example, if `johndoe@gmail.com` signed up before we added Google login, then tried to use his Google account to login via OAuth, Sorcery does not check if the user exists first. This triggers a database exception violating our unique index on email address, which we have to rescue from. We could  pass in a block that checks if the user exists first, but we can't pass in custom logic for using an existing record.


## The Cleanup

Sometimes the most exhilarating part of software development is deleting old crufty code. In this exercise we get to delete all Devise-related components that we've overridden over the years, along with the "magic" calls in our routes and `User` model. That feels good!


## Wrapping Up

In hindsight, the migration process was mostly painless. We had to write more code but now all of the important logic is exposed and expressed in our own local conventions - and we understand all of it! It'll be significantly easier to debug that next head-scratching bug or upgrade other core packages.


<br>
![Art showing a wizard at a gate](/assets/images/posts/2024-08-23/wizard-at-gate.jpg){:.smooth-corners .full-width}
