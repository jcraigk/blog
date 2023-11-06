---
title: Sprockets to Shakapacker
date: 2023-10-06 12:00:00 -0700
tags: software ruby rails
header:
  image: /assets/images/posts/2023-10-06-header.jpg
  teaser: /assets/images/posts/2023-10-06-header.jpg
---

This article describes the process of migrating a Ruby on Rails app from Sprockets to Shakapacker. You can view the entire change set on GitHub:

* [jcraigk/phishin - Shakapacker #323](https://github.com/jcraigk/phishin/pull/323)
* [jcraigk/phishin - Shakapacker support #324](https://github.com/jcraigk/phishin/pull/324)

## The Problem with Assets

If you've been developing web applications for a while, you know what a pain it is to manage your assets. Assets include all of the pieces that make your frontend user experience work beyond the initial HTML payload. These include images, stylesheets, and Javascript. Delivering these efficiently to the end user while supporting a pleasant development experience is no easy task.

Historically, the Ruby on Rails approach has been to use the [Sprockets](https://github.com/rails/sprockets) gem to manage assets. This is a nice lib that provides reasonable configuration options for common situations. If your site does not rely on much Javascript state management, this will work fine. However, many modern frontends have complex state management handled by Javascript that fetches data from a JSON API. If you're in this situation, then Sprockets may not be powerful enough.

[Webpack](https://webpack.js.org/) is a popular Javascript bundling lib that is embraced across many web frameworks. Previously, the [Webpacker](https://github.com/rails/webpacker) Ruby gem provided a first class Javascript experience on the backend for Rails apps. That gem has been retired but the work has continued with [Shakapacker](https://github.com/shakacode/shakapacker).


## Sprockets or Shakapacker?

The official Rails releases have waffled on the two approaches of Sprockets vs Webpack. Some engineers even suggest using Webpacker/Shakapacker to manage your Javascript and Sprockets to manage styles and images. While this can work, using multiple systems for asset management can lead to developer confusion (including your own) down the road. Reducing gem dependencies is also preferable.

One of the projects I maintain is an [audio streaming website](/projects/03-phishin.html) that provides a persistent audio player while the user browses the content. Think Spotify or iTunes on a web page. I implemented the dynamic parts of this using [jQuery wrapped in CoffeeScript classes](https://github.com/jcraigk/phishin/tree/f1c1f235c61ed389a02403dcf4c54d663a6d246a/app/javascript/src/coffeescript) in 2013. Back then, CoffeeScript was the conventional way of writing JS in Rails and jQuery was still a popular lib for manipulating the DOM. Times have changed and the frontend world has matured significantly in the last decade. Now, it is generally frowned upon to use jQuery at all, and component-based frameworks like React have taken over.

Let's assume you want to build a React frontend for your existing JSON API implemented in Rails. You have a couple of options for managing all of that Javascript you'll be writing: [react-rails](https://github.com/reactjs/react-rails), which works well with Sprockets, or [react_on_rails](https://github.com/shakacode/react_on_rails) which requires Shakapacker. The latter sports several more capabilities out of the box including server side rendering with routing and code splitting.

I began building a simple React UI as a mobile version of the streaming website. I started with Sprockets and `react-rails`. It was pretty easy to setup and I got a basic browsable list of content on my screen quickly by following the React documentation. Then I wanted to get a bit more advanced and use React Router, which comes in a separate Javascript package called ReactDOM.

This is where things got sticky. With Sprockets, there is no Javascript package manager, no `package.json`. All of your Javascript assets need to either be wrapped in a gem that you include in your `Gemfile` or pulled in manually and placed in a `/vendor` folder. You can also use raw `<script>` tags in your layout header, but that adds development complexity and can affect app performance.

For using React Router, the [official wiki](https://github.com/reactjs/react-rails/wiki/Using-react-router) of `react-rails` instructs developers to manually download the necessary JS package, place it in a `/vendor` folder, include it in `application.js` if necessary, and globalize the JS with lines like `var Router = ReactRouter.Router;`. This isn't too painful, but there a few suboptimal things going on here. First, there is no version management around this lib. I will have to manually keep track of its versioning and manually pull down new versions when I want to update. Second, this library code now gets checked into my repo, which is not ideal. Finally, modern Javascript practices frown on using `var`, especially to globalize access. All of this is starting to seem outdated.

Let's take a look at another situation. Let's say there's a gem maintainer who packages up the React Router lib for you so you can use Bundler for managing that asset in Ruby land. That solves the version and packaging issues, but now you must rely on the gem maintainer to keep the underlying JS libs up to date. Not ideal. What you really want is direct access to those JS libs with first class package management.

With Shakapacker, your assets are compiled using Javascript, not Ruby. Your frontend dependencies will be managed by Yarn, not by Bundler. You'll be free to update all of your Javascript independently of any gem maintainers. This power does come with some tradeoffs which we'll explore as we migrate our audio streaming website to Shakapacker.

## Swap the Gems

First, we'll want to replace `sprockets` and other asset-related gems from our `Gemfile` and replace them with the `shakapacker` gem. In my project I was able to remove the following gems

```
gem 'bootstrap-will_paginate'
gem 'coffee-rails'
gem 'execjs'
gem 'jquery-rails'
gem 'jquery-ui-rails'
gem 'sass-rails'
gem 'soundmanager2-rails'
gem 'twitter-bootstrap-rails'
gem 'uglifier'
```

and replace all of those with the single line

```
gem 'shakapacker'
```

[View this change on Github](https://github.com/jcraigk/phishin/pull/323/files#diff-d09ea66f8227784ff4393d88a19836f321c915ae10031d16c93d67e6283ab55f).

We're already seeing how this is cleaning up our package management and will lead to separation of backend and frontend concerns. Feels good so far!


## Shakapacker Installer

Next we'll run the Shakapacker installer

```
rails shakapacker:install
```

If you see errors like `undefined method 'assets'`, then you'll need to go into your `config/environment*` files and remove all references to `config.assets`. You can also delete `config/initializers/assets.rb`. Then run the installer again.

This will setup our initial config files and kick off the Yarn package manager to pull in basic dependencies.


## Managing JS Packages with Yarn

We're still going to need the Javascript libraries wrapped in those gems we removed earlier. So we'll need to find the corresponding NPM packages and install them with Yarn.

For most of your dependencies, this should be a painless process. Simply use `yarn add` to include all of the packages you need to run your frontend. Here is what I ran

```
yarn add coffeescript coffee-loader
yarn add sass sass-loader
yarn add bootstrap@3.4.1
yarn add jquery jquery-ujs jquery-ui jquery.cookie
yarn add soundmanager2
```

You should prefer the most recent stable versions of libs, pinning to old versions only when you need to. In my case, migrating to Bootstrap v4 would have taken more manual testing than it was worth given my plan to replace that framework with an alternative in the medium term.

This part of the process can be tricky for older projects as you may find a situation where a gem wrapped a JS library version that is no longer available in NPM. I found this to be the case with the `twitter-bootstrap-rails` gem. I had it pinned at 2.2.8. Inspecting the gem source at that version I saw that it was pulling in Twitter Bootstrap 3.1.1. Sadly, that version was EOL'd so long ago that it is no longer available as an NPM package.

This situation is likely the most time consuming you will run into during the migration process, but it also highlights weak points in your system that have been neglected. In my situation I upgraded to the next version of Boostrap using `yarn add bootstrap@3.4.1`. This caused some visual glitches on the frontend I had to fix one by one. Most of it involved changing margins/padding and removing some outdated class names on dropdown menus.


## File Locations

With Shakapacker, the default path for storing assets is `app/javascript`. This includes images and stylesheets 🤔. In the past I've used `app/webpacker` as that seemed like a better name, but the `app/javascript` convention has been adopted so widely that I now just use the standard path and ignore the conflict in my brain when I see `app/javascript/images/photo.jpg`. If you want to change it, edit the `source_path` option in `config/shakapacker.yml`.

You'll need to move all of your JS, CSS, and image files from their old spots in `app/assets` into their new paths at `app/javascript`. Javascript files themselves should be placed in `app/javascript/src` or a similar sibling directory (your choice). I ended up placing my CoffeeScript files in `app/javascript/src/coffeescript`.


## Manifest.js

Sprockets v3 introduced the `app/assets/config/manifest.js` file which allows you to list out specific files you want compiled. In Shakapacker, a file of the same name gets generated by the compile process but that's not controlled by the developer. Simply delete the Sprockets `manifest.js` file along with the entire `app/assets` folder after you move your JS, CSS, and images to `app/javascript`.


## Packs

With Shakapacker, you'll place the JS and CSS files you'll include in your application in the `app/javascript/packs` folder. Think of these as roots of a tree that will pull in all of the other things they need to create the final pack of assets you'll send down to the client. Generally there will be one for JS and one for CSS.

Here's what I ended up with in my `app/javascript/application.js` file.

```
// Images
const images = require.context('../images', true)
const imagePath = (name) => images(name, true)

// Global dependencies
import 'jquery/src/jquery';
import 'jquery-ujs'
import 'bootstrap/dist/js/bootstrap';
import 'soundmanager2'

// App logic (legacy CoffeeScript)
import '../src/coffeescript/app.js.coffee';
```

[View this change on GitHub](https://github.com/jcraigk/phishin/pull/323/files#diff-a8ec38e35d90d021510296965c5b8a1dc2bf98750d0859cd9ea64e34d17c36ff)

The first part tells Shakapacker where all of the images are. These can be included using asset helpers (see below).

The second part pulls in global dependencies that I added using `yarn add`. All of these exist in my `node_modules` folder. You can easily open that folder, inspect the contents, and find the files you need to include. Look for `dist` or `src` folders if documentation is lacking.

The last part pulls in the business logic of the app, which was written using CoffeeScript classes. Note that here we're importing only a single `app.js.coffee` file since it imports all of its own dependencies. More on how I had to refactor these later.

Here's what my `app/javascript/application.css.scss` file looks like

```
@import '~jquery-ui/themes/base/all.css';
@import '~bootstrap/dist/css/bootstrap.css';

.my-style {
  size: 10px;
}
...app styles...
```

[View this change on GitHub](https://github.com/jcraigk/phishin/pull/323/files#diff-6c1d2661110c4e1f4951577a5877ca95d62169fe4616966b558c46120adc97fd)

Note the import values start with `~`. Just like with the JS, you can find these in your `node_modules` folder. Nothing mysterious, just files on your disk managed by Yarn.

Both of these files get included into your layout using view helpers just as with Sprockets

```
# app/layouts/application.html.erb

<%= Javascript_pack_tag 'application' %>
<%= stylesheet_pack_tag 'application' %>
```

[View this change on GitHub](https://github.com/jcraigk/phishin/pull/323/files#diff-be39e2eefda05880ba909b9122579462b3c758837273de6057d97631e9245843)


## View Helpers

In Sprockets there are view helpers like `asset_url` that are used to generate the HTML that the client uses for loading the assets. There are similar helpers in Shakapacker, but they are named differently. For example, `Javascript_pack_tag` vs `Javascript_include_tag`.

One caveat is that Shakapcker references images as if placed in a `static` folder so for example

```
image_pack_tag('static/images/icon-relisten.png')
```
references an image stored in

```
app/javascript/images/icon-relisten.png
```

You'll want to search for all occurrences of the older Sprockets helpers and replace them with their Shakapacker equivalents. This can often be done with search and replace in your editor.

## Refactoring JS into Modules

In modern JS, block-scoped variables (`const/let`) are preferred over `var` and the module pattern (`export/import`) is preferred over using the global namespace, which can lead to naming collisions and unpredictable behavior. When you package your assets with Shakapacker, any legacy code that does not adhere to these patterns can be problematic. In my situation, I have some legacy CoffeeScript that needs to stick around while I build out a React replacement. Luckily, CoffeeScript handles the variable issues but I was relying on global namespacing for including my CoffeeScript classes.

The changes were straightforward. My main class used to look like this

```
@App = {}

$ ->
  App.Util     = new Util
  App.Player   = new Player
  App.Playlist = new Playlist
  App.Map      = new Map

  ...busines logic...
```

Here we're setting a global object called `App` and relying on the presence of `Util`, `Player`, `Playlist`, and `Map` implicitly inside our jQuery onReady (`$ ->`) function. Where did these come from? Well, Sprockets bundled them for us and put them in the global namespace. That's not going to work with Shakapacker. Instead, we need to export `App` as a module and import the other dependencies as modules too.

Here's our updated code

```
import Map from './map.js'
import Player from './player.js'
import Playlist from './playlist.js'
import Util from './util.js'

App = {}
export default App

$ ->
  App.Util     = new Util
  App.Player   = new Player
  App.Playlist = new Playlist
  App.Map      = new Map

  ...busines logic...
```

And if we take a look in our `Util` class in `util.js`, we now have

```
class Util
  ...busines logic...

export default Util
```

After making that change to each CoffeeScript class, the business logic still works and we're not littering global namespace. Nice!

[View this change on GitHub](https://github.com/jcraigk/phishin/pull/323/files#diff-710eb655ce1e05e0ab824308e25a3a08286a48f9a7aa3cee429ded20d85999d0)


## Shakapacker CLI

It can be frustrating when your assets are not compiling. Most experienced Rails devs have run into situations where an asset compilation failure brings development to a standstill. Debugging this can be time consuming process, especially in CI build environments.

In Sprockets, when you run `rails assets:precompile`, Ruby is driving the bus. But with Shakapacker, you're actually running a thin wrapper around `webpack.js`, so you get all of the verbose output from Webpack as your assets are compiled. Here's a tail of a successful build

```
asset modules 714 bytes (Javascript) 133 KiB (asset)
  optional modules 420 bytes (Javascript) 104 KiB (asset) [optional]
    ./app/javascript/images/icon-context.png 42 bytes (Javascript) 236 bytes (asset) [optional] [built] [code generated]
    + 9 modules
  + 7 modules
webpack 5.88.2 compiled successfully in 1487 ms
```

This level of detail is hidden behind a few layers of Ruby when you're running Sprockets. You can redirect Sprockets logging to the Rails logger, but you still don't get the kind of verbosity you get with Webpack.

Another nicety here is that you'll get warnings if your asset packs exceed recommended sizes, which helps you keep your app performant.

Shakapacker also comes with `bin/shakapacker-dev-server`, which wraps `webpack-dev-server.js`. This adds development capabilities including hot module reloading, which can significantly speed up development of large projects.


## Build Config

Adding Shakapacker also means adding a Javascript runtime as a hard dependency for your app. Previously we were relying on the `execjs` and `coffee-rails` gems to handle CoffeeScript transpilation but now Shakapacker will be handling this using the packages we loaded with Yarn.

If we're running our app natively, that means we need a Javascript runtime and Yarn installed. Try [asdf version manager](https://asdf-vm.com/) if you're running your Rails app natively.

If you're running in Docker, you'll need to add a few lines to your `Dockerfile`. For this project I ended up needing a specific version of Node, which I can bump that later using `$NODE_VERSION`. Here's what I added to the `Dockerfile`

```
# Install a specific version of nodejs using nvm for yarn install
ENV NODE_VERSION 14.18.0
RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash && \
    . $HOME/.nvm/nvm.sh && \
    nvm install $NODE_VERSION && \
    nvm alias default $NODE_VERSION && \
    nvm use default
ENV PATH $PATH:/root/.nvm/versions/node/v$NODE_VERSION/bin
RUN curl -o- -L https://yarnpkg.com/install.sh | bash
ENV PATH="/root/.yarn/bin:/root/.config/yarn/global/node_modules/.bin:$PATH"

...bundle install...

COPY package.json yarn.lock ./
RUN yarn install
```

[View this change on Github](https://github.com/jcraigk/phishin/pull/324).


## Wrapping Up

Converting from one asset management system to another is never simple, it requires careful attention during each step. You'll need to weigh the time investment vs the payoff. The decision to migrate or not comes down to a somewhat subjective question: Does your app rely on a lot of state management on the client side?

If the answer is yes, it's probably worth converting to Shakapacker so you gain that first class Javascript experience to match the first class Ruby experience that modern Rails provides. If the answer is no, then it's fine to keep using Sprockets and the popular gems that wrap the JS libs you need. Focus on more important parts of your application or business instead!

For this project, the answer was a resounding "yes" so this migration was well worth it. Overall I found the process to be pretty pleasant. Shakapacker seems mature, [well documented](https://github.com/shakacode/shakapacker) and well maintained. I'm looking forward to not having to migrate to a different asset manager for a while.

Thanks to the maintainers of all the software mentioned here! Well done.

<br>
![Art showing organized shelves](/assets/images/posts/2023-10-06/organized-assets.jpg){:.smooth-corners .full-width}
