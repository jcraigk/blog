---
title: KudoChest
excerpt: An open source social engagement app for Slack and Discord
header:
  image: /assets/images/projects/kudochest-header.jpg
  teaser: /assets/images/projects/kudochest-header.jpg
---

In 2016, I watched [*Nosedive* (Black Mirror)](https://en.wikipedia.org/wiki/Nosedive_(Black_Mirror)), and it freaked me out. It depicts a society where people rate each other on a five-star scale for nearly every interaction. This, unsurprisingly, leads to both humorous and horrifying outcomes.

From one perspective, I can see the appeal of a meritocracy with central accounting — something that feels a bit like status quo. However, taking it to the extreme as depicted in *Black Mirror* is clearly going too far. Right? Or is that exactly where we're headed? Honestly, I'm not sure.

This episode got me thinking about software that manages social status and notoriety. My initial idea was to create a website that allowed people to send karma points between email addresses, but the concept was too broad to be practical. Over the next few years, as I used Slack and Discord extensively, I noticed how various apps were implementing ratings and karma systems. Each had its own approach, and none seemed to fit all scenarios. This led me to create a flexible app that could adapt to an existing culture and enhance it organically.

I started developing an app called *KarmaChest*, which had two main components: a website and a chatbot. The chatbot could be integrated with Slack or Discord, while the web component was designed for administration, user profiles, and other UI niceties. The chatbot served as an interface within Slack, allowing users to give kudos (or karma) and query the system for leaderboards, stats, and other features. I built the app using the [Ruby on Rails](https://rubyonrails.org/) stack because I'm familiar with it and wanted to prototype quickly.

Early on, I realized I'd need to cache the state of users, channels, and other entities for each team. This would enable fast local lookups instead of repeatedly querying the chat APIs for common requests.

After working on the project for about 14 months, I began advertising it on forums and sharing it with other engineers. Eventually, I convinced my employer — a publicly traded company with approximately 1,200 employees — to replace our aging [Hubot](https://hubot.github.com/) karma tracker with *KarmaChest*. It was a hit, so I've continued maintaining the project. Along the way, I renamed it *KudoChest* because "karma" has religious connotations, and "kudos" feels like a better fit.

**Takeaways:**
- Slack's API, customer support, and documentation are excellent.
- Discord's API, customer support, and documentation were subpar in 2018–2019.
- It's incredibly rewarding to see hundreds of coworkers giving each other kudos daily.
