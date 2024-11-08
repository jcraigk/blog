---
title: A Good Stack
date: 2024-11-07 12:00:00 -0700
tags: software ruby rails react
header:
  image: /assets/images/posts/2024-11-07-header.jpg
  teaser: /assets/images/posts/2024-11-07-header.jpg
---

BUTTHEAD: Beavis, I have seen the top of the mountain, and it is good.
{:.quote}

TLDR: Try [React on Rails](https://github.com/shakacode/react_on_rails) for your next web app.

When you've been at something for over twenty years, you get a feel for things. You sense old patterns lurking in new tools and are wary of the new shiny objects that the kids are raving about. Your toolbox is full of boring but highly reliable pieces of software that have earned their place through valiant battle testing.

We know the players. On the backend: Rails, Laravel, Django etc. and on the frontend: Vue, Angular, React, and a few others.

If you're starting a new project, choosing from this list of options can feel overwhelming. During the last decade I've seen many companies choose TypeScript or some flavor of JS on the server. Their rationale is based on the concept of  "one language everywhere," enabling the same developers to seamlessly transition from backend to frontend. Since we're stuck with Javascript on the frontend, let's use it on the backend, why not?

Well, it's rare to find a high quality "full stack" engineer these days, given the expectations about modern apps. There is so much to know on both ends of the stack that if you're building a serious software company, you'll want specialized engineers working in specific areas. You wouldn't expect a .NET geospatial search engineer to work on React UI animations with no ramp up. But if you're a smaller company, sometimes you have no choice when allocating resources around the project, and indeed having one language eases the transition even if the intellectual domains differ.

Until ChatGPT and similar LLMs arrived, I think that was a solid justification for choosing JS on the backend. But now with the assistance in both explanation as well as code generation that LLMs provide, language heterogeneity is no longer  a major liability. In fact, human engineers don't need to know a language inside and out to write high quality code or to comprehend a codebase. Many of us should abandon our tight specializations (mine was backend/database) and embrace the full stack again.


## The Backend

The language you choose on the backend is highly dependent on the app you're building. If you need to squeeze concurrent performance out of your hardware, you'll likely choose Go or Elixir. But if runtime performance is less of a concern and you want software that is easy for humans to read, write, reason about, and change, I firmly believe that Ruby on Rails is the best option for building web backends.


### Why Rails?

The primary reasons to use Rails are:
 * Software maturity
 * Developer community
 * Ruby's syntax

 Rails is one of the oldest and most respected frameworks out there. It has influenced every other modern framework and continues to receive major improvements from a large team of seasoned veterans. It has best in class components such as ActiveRecord, which makes interacting a relational database a joyful experience, and ActiveStorage, which simplifies what was once a complex task of managing file attachments. These two components alone are worth the price of admission, and they just scratch the surface of the high quality libraries available in the Rails ecosystem.

With large influential tech companies like Shopify and GitHub continuing to invest in Ruby and Rails, the framework is bound to enjoy popularity and relevance long into the future. This means it's a solid choice for building products and teams around.


## Why Ruby?

Ruby is almost 30 years old. Its ethos is based on developer happiness and the principle of least surprise. It's a sharp flexible tool with strong idiomatic conventions. It lets you do what you need to in the way you want to do it. You can certainly get yourself into trouble using Ruby, make no mistake. It is not "locked down" as some other languages like Java are. It has sharp edges that will nick the unwary developer.

One of Ruby's best features is its flexible syntax, allowing it to easily produce domain specific languages (DSLs), which are handy in many server side situations. Paired with Rubocop, Ruby's excellent linter, different idioms can be enforced to get the most out of the one language in different contexts. Ruby's great for shell scripting, data processing, and writing specs in addition to be a great application language.

Ruby's object model make it easy to alter any code during runtime and its metaprogramming features enable dynamic APIs that are difficult or impossible to implement in other languages. It's open, flexible, and builder friendly.


## Gems

Ruby has a mature set of libraries called gems built by the community. Rails is only one of them. Other mature gems like [GrapeAPI](https://github.com/ruby-grape/grape) and [Grape Entity](https://github.com/ruby-grape/grape-entity) make building RESTful APIs a snap. Grape automatically generates Swagger documentation, which means you get interactive documentation for free with your well formed API codebase. Working with these tools is simply a joy, especially if you let an LLM write the boilerplate and assist with implementation details and debugging.


## CSS and Javascript

If you're building a web app, you have to deal with client presentation logic from the server in some way, whether you're building HTML and sending it over the wire or managing a set of Javascript and CSS.

For years, Rails shipped with Sprockets, which is a Ruby based approach to managing these assets. It now ships with [Propshaft](https://github.com/rails/propshaft), which is a modernized asset manager also implemented in Ruby. Rails officially supports [StimulusJS](https://stimulus.hotwired.dev/) for adding Javascript functionality to server-side rendered apps. This combo works well for simple sites with little or no frontend state. However, to add javascript libraries with Sprockets or Propshaft, you need to bundle those into a gem, adding an extra layer of maintenance.

Alternatively, using Javascript to compile CSS and JS on the backend can be very handy when you're implementing most or all of your frontend UX in React. Using [NPM](https://www.npmjs.com/) or [Yarn](https://yarnpkg.com/) to manage JS dependencies is more ergonomic than using Bundler and gives you access to the best JS libraries as they're released without having to wait for a gem maintainer. This is the approach that [React on Rails](https://github.com/shakacode/react_on_rails) takes. It replaces Sprockets/Propshaft with [Shakapacker](https://github.com/shakacode/shakapacker), which is an extension of the Webpacker project.

As the web has matured, so have users' expectations around client side features. Libraries like React have burst onto the scene to satisfy these expectations. I've built sites in almost all of the frontend frameworks and have found React to offer the best development experience. I like its component model and rich set of community plugins. Combining logic with presentation as JSX may feel strange at first, but it pays dividends when you're dealing with even moderately complex state on the frontend.

React on Rails works cleanly with zero configuration, providing a set of methods on the Rails side for exposing your React app to the client. It also supports server side rendering out of the box, which is often an important feature for SEO and performance purposes and can be difficult to setup manually.

Building React components with hot module reloading enabled is a breeze, eliminating the need to hit refresh in the browser when CSS or JS changes, maintaining state and DOM inspection in the process. This has significantly sped up my development time.


## A note on LLMs

Using frameworks and adhering to  conventions is more valuable than ever now that much of our development time is spent interacting with LLMs and copying their code rather than writing code ourselves. The LLM you're working with will have a vast knowledge of code written in Rails and React and can be very effective at producing high quality implementations with even low quality prompts and examples.

Over the last year I've begun to rely on ChatGPT for producing most of the code I've committed rather than just asking it for help. This process will almost certainly continue until LLMs will be able to comprehend entire codebases with ease.

## Try Rails

Just today, [Rails 8](https://rubyonrails.org/2024/11/7/rails-8-no-paas-required) was released, shipping with powerful new devops tools for deploying your app to production environments. There's never been a better time to start a project on Rails or migrate an old krufty v1 of a system over to something modern and  reliable.


<br>
![Art showing sunrise over a mountain](/assets/images/posts/2024-11-07/sunrise-over-mountain.jpg){:.smooth-corners .full-width}
