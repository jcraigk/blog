---
title: KudoChest
excerpt: An open source social engagement app for Slack and Discord
header:
  image: /assets/images/projects/kudochest-header.jpg
  teaser: /assets/images/projects/kudochest-header.jpg
---

As the modern workplace has shifted from traditional office settings to remote (usually from home), so too have the tools we use to interact. In the early 2000's, we used to gather around the water cooler or lunch table to strengthen social bonds with our coworkers. As time moved on, we began to use email and instant messaging more often to stay socially connected. As this shift occurred, we lost much of the subtle but relevant communication that occurs between physically proximate people - body language, tone, and realtime reaction. Emojis, acronyms ("lol", etc), and video meetings have recaptured some of this, but remote communication in 2024 is a far cry from those face-to-face interactions that we took for granted 20 years ago.

![Black Mirror logo](/assets/images/projects/kudochest/black-mirror.jpg){:.image-centered}

In 2016, I watched an episode of [*Black Mirror*](https://en.wikipedia.org/wiki/Black_Mirror) called [*Nosedive*](https://en.wikipedia.org/wiki/Nosedive_(Black_Mirror)), and it freaked me out. It depicts a society where people rate each other on a five-star scale after nearly every interaction, however slight. This, unsurprisingly, leads to both humorous and horrifying outcomes. From one perspective, I can see the appeal of a meritocracy with central accounting — something that feels a bit like status quo. However, taking it to the extreme as depicted in this episode is clearly going too far. Right? Or is that exactly where we're headed? Honestly, I'm not sure.

This episode, along with the shift to remote work, got me thinking about software that facilitates status and notoriety in a social group. My initial idea was to create a website that allowed people to send karma points between email addresses, but the concept was too broad to be practical. Over the next few years, as I used Slack and Discord extensively for work and social recreation, I noticed how various apps were implementing ratings and karma systems. Each had its own approach, and none seemed to fit all scenarios. This led me to create a flexible app that could adapt to an existing culture and enhance it organically.

![KudoChest login screenshot](/assets/images/projects/kudochest/login-page.jpg){:.image-centered}

I started out by developing an app called *KarmaChest*, which had two main components: a website and a chatbot. The chatbot could be integrated with Slack or Discord, while the web component was designed for administration, user profiles, and other UI niceties. The chatbot served as an interface within Slack, allowing users to give kudos (or karma) and query the system for leaderboards, stats, and other features. I built the app using the [Ruby on Rails](https://rubyonrails.org/) stack because I was most familiar with it and wanted to prototype quickly.

![KudoChest leaderboard screenshot](/assets/images/projects/kudochest/leaderboard.jpg){:.image-centered}

To optimize performance, I implemented a caching system using [PostgreSQL](https://en.wikipedia.org/wiki/PostgreSQL) and [Redis](https://en.wikipedia.org/wiki/Redis). When a team initially signs up, the system queries various chat platform APIs to fetch their users, channels, and other organization data. These entities are stored locally, enabling quick lookups without repeatedly hitting the external APIs. The cache stays current by listening to webhook callbacks from the chat platforms, which notify us of any updates to these entities.

After 14 months of development, I open sourced the code ([GitHub](https://github.com/jcraigk/kudochest)) and promoted it on various online forums. I rebranded it as KudoChest, replacing "karma" with "kudos" to be more inclusive and to respect those who consider karma a sacred concept.  I successfully pitched it to my employer - a public company of roughly 1,200 people - as a replacement for our outdated Hubot karma tracking system. Its overwhelming success there motivated me to maintain the project further.

![KudoChest history screenshot](/assets/images/projects/kudochest/history.jpg){:.image-centered}

While I have moved on to other projects since leaving that employer, it was a gratifying experience to see my creation appear in every channel across the organization. One of my favorite use cases was when a new employee would come on board and immediately feel a sense of acceptance as longtime employees welcomed them by giving them kudos. The leaderboard seemed to accurate reflect real social capitol at the company - those at the top of the board were the friendly and helpful folks from departments like quality assurance as opposed to those at the top of the org chart who wielded actual power.

As a [Swiftie](https://en.wikipedia.org/wiki/Swifties) I feel it's appropriate to leave you with these lyrics:

<div class="quote">'Cause karma is the thunder
Rattling your ground
Karma's on your scent like a bounty hunter
Karma's gonna track you down
Step by step from town to town
Sweet like justice, karma is a queen
Karma takes all my friends to the summit
Karma is the guy on the screen
Coming straight home to me
&mdash;Taylor Swift
</div>


**Takeaways:**
- Slack's API, customer support, and documentation were excellent in 2018–2019.
- Discord's API, customer support, and documentation were subpar in that timeframe.
- Seeing hundreds of daily kudos exchanges between coworkers proved deeply rewarding
- Building a fully integrated, high-quality app takes far more time than initially estimated

![KudoChest logos](/assets/images/projects/kudochest/logos-andy-warhol-style.png){:.image-centered .centered}
