---
title: GigTablet
excerpt: An app for gigging musicians that manages songs and setlists
header:
  image: /assets/images/projects/gigtablet-header.jpg
  teaser: /assets/images/projects/gigtablet-header.jpg
---

As someone with generally bad memory for chords and melodies, I need notes when I'm gigging. Chords, lyrics, melodies, etc. For years I used Apple MainStage for this purpose. On the left was a list of songs and on the right were the notes for each one, a simple and effective setup. This provided quick searching and immediate access to notes for each song.

I noticed that some other musicians at the time were using Google Docs to store their song charts. They would setup tables of contents to jump to specific songs. This works, but it's cumbersome and error prone. If you give someone else edit access, they might mess up your notes.

Unfortunately MainStage does not have an iOS version so for several years I simply lugged my laptop onstage. These days (2023), that looks a little clunky compared to a tablet, so I experimented with mirroring my laptop screen. This worked alright but MainStage has extra UI I didn't want and the extra burden of the laptop plus tablet was not ideal.

To solve these issues, I built [GigTablet](https://gigtablet.com/). This is a simple progressive web app (WPA) written in [Rails](https://rubyonrails.org/) that lets groups of artists share a repertoire, manage their own notes, build setlists, and keep coordinated during live performance.

![GigTablet screenshot](/assets/images/projects/gigtablet/screenshot-1.png){:.smooth-corners}

We've been experimenting with the app while gigging in the soul funk band [OC Funk Collective](/projects/oc-funk-collective). The horn players have been able to eliminate a lot of paper rustling on stage and I've reduced physical and visual clutter.

![GigTablet screenshot](/assets/images/projects/gigtablet/screenshot-2.png){:.smooth-corners}

Takeaways:
  * ChatGPT is a pretty good engineering partner, especially in unfamiliar territory
  * Progressive web apps (PWAs) are sadly under supported by browsers and OS's
  * You can't expect horn players to scan their own documents (I kid, I kid)
