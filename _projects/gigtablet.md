---
title: GigTablet
excerpt: GigTablet etc etc
header:
  image: /assets/images/projects/gigtablet-logo-wide.png
  teaser: /assets/images/projects/gigtablet-logo-wide.png
gallery:
  - url: /assets/images/unsplash-gallery-image-1.jpg
    image_path: assets/images/unsplash-gallery-image-1-th.jpg
    alt: "placeholder image 1"
  - url: /assets/images/unsplash-gallery-image-2.jpg
    image_path: assets/images/unsplash-gallery-image-2-th.jpg
    alt: "placeholder image 2"
  - url: /assets/images/unsplash-gallery-image-3.jpg
    image_path: assets/images/unsplash-gallery-image-3-th.jpg
    alt: "placeholder image 3"
---

As someone with generally bad memory for chords and meloides, I need notes when I'm gigging. Chords, lyrics, melodies, etc. For years I used Apple MainStage for this purpose. On the left was a list of songs and on the right were the notes for each one, a simple and effective setup. This provided quick searching and immediate access to notes for each song.

I noticed that some other musicians at the time were using Google Docs to store their song charts. They would setup tables of contents to jump to specific songs. This works, but it's cumbersome and error prone. If you give someone else edit access, they might mess up your notes.

Unfortunately MainStage does not have an iOS version so for several years I simply lugged my laptop onstage. These days (2023), that looks a little clunky compared to a tablet, so I experimented with mirroring my laptop screen. This worked alright but MainStage has extra UI I didn't want and the extra burden of the laptop plus tablet was not ideal.

To solve these issues, I built [GigTablet](https://gigtablet.com/). This is a simple progressive web app (WPA) written in [Rails](https://rubyonrails.org/) that lets groups of artists share a reportoire, manage their own notes, build setlists, and keep coordinated during live performance.

We've been experimenting with the app while giging in the soul funk band [Rat Soup](https://www.ratsoupforthesoul.com/). The horn players have been able to eliminate a lot of paper rustling on stage and I've reduced physical and visual clutter.

Lessons learned:
  * ChatGPT is a pretty good engineering partner, especially in unfamiliar territory
  * Progressive web apps (PWAs) are sadly under supported by browsers and OS's
  * You can't expect horn players to scan their own documents (I kid, I kid)
