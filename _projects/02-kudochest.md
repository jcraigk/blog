---
title: KudoChest
excerpt: A social engagement app for Slack and Discord
header:
  image: /assets/images/projects/kudochest-header.png
  teaser: /assets/images/projects/kudochest-header.png
---

In 2016 I saw [Nosedive (Black Mirror)](https://en.wikipedia.org/wiki/Nosedive_(Black_Mirror)) and it freaked me out. It depicts a society in which people rate each other on a 5-star scale for nearly every interaction they have. This of course produces humorous and horrifying outcomes.

From one perspective I see the value in living in a meritocracy with central accounting. In many respects, we live in one today. However, taking it to the extreme as depcited in the Black Mirror episode is clearly going too far. Right? Or is that exactly where we are headed? I'm not sure, to be honest.

Seeing this episode got me thinking about software that manages social status and notoriety. My original vision was to make a website that could be used to send karma points between email addresses, but this idea provided too broad to be useful. I was using Slack and Discord a lot in the years that followed and I was noticing how various apps were implementing ratings or karma. There were various approaches and I didn't see a one size fits all solution. So I set out to create a flexible app that could be fit into an existing culture to enhance it organically.

I started building an app called KarmaChest which had two parts: a website and chat bot. The chat bot could be installed in Slack or Discord. The web portion would be used for administration, pretty profile pages, and other UI niceties. The chat bot serves as an interface from the Slack client to give kudos/karma and query the system for leaderboards, stats, and other info. I used the standard [Ruby on Rails](https://rubyonrails.org/) stack because I'm familiar with it and wanted to rapidly prototype.

I quickly realized that in order to deliver some of the features I wanted to build, I'd need to cache the state of users, channels, and other entities for each team. This would enable quick local lookup rather than having to be constantly hitting the chat APIs for common queries.

I worked on the project for about 14 months before I started advertising it on forums and with other engineers. I was able to convince my employer, a publicly traded company with approximately 1,200 employees, to install it in place of our aging [Hubot](https://hubot.github.com/) karma tracker. It ended up being quite a hit, so I've continued to maintain the project. It was renamed KudoChest since "karma" has religious associations and "kudos" is a better fit anyway.

Takeaways:
  * Slack's API, customer support, and documentation are all very good
  * Discord's API, customer support, and documentation are not good (or at least they were not in 2018-2019)
  * It's gratifying to see hundreds of your coworkers giving each other kudos on a daily basis
