---
title: PeepMode
excerpt: A spectator mod for Starcraft II
header:
  image: /assets/images/projects/peepmode-logo-wide.png
  teaser: /assets/images/projects/peepmode-logo-wide.png
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

PeepMode is a mod for [StarCraft II](https://en.wikipedia.org/wiki/StarCraft_II) released in May 2011. The [original Team Liquid post](https://tl.net/forum/sc2-maps/223176-mod-peepmode-ultra-spectator-maps) describes the initial release and feedback from players. At first, issues with the UI prevented many from enjoying it, but after some improvements it became one of the most popular mods on [Battle.net](https://en.wikipedia.org/wiki/Battle.net). It reached the #1 spot and stayed there for a few  weeks in 2011.

I stopped personally maintaining the project in 2016 but it's still maintained by a dedicated group. You can [browse the GitHub repo](https://github.com/Kelzorz/PeepMode) or [join the Discord](https://discord.gg/hJ7wR7uk) if you're interested in playing or contributing.

The mod was created entirely in the [StarCraft II Editor](https://s2editor-guides.readthedocs.io/New_Tutorials/01_Introduction/001_Editor_Introduction/). Using the SC2 Editor involves a combination of point-and-click UI interaction along with traditional programming in a C-like environment called Galaxy. This get bundled with custom assets and published to [Battle.net](https://battle.net), where it becomes available for other players to discover and play.

The motivation for this project was, at the time, my love of competitive gaming and my passion for Starcraft II in that space. I had been playing the original Starcraft with friends since its release and had invested over a hundred hours playing SC2 when I started looking at the modding scene. There was a mod on Battle.net that allowed up to ten players to join a game and watch 2 of the players compete while the others chatted. This basic feature was missing from Battle.net itself and I found it compelling. I tried to contact the author of the mod, but got no response, so I started looking at building something myself.

A few design goals:
  * Comprehensive overhaul of versus style play in Battle.net allowing spectators
  * Graphical faceoff UI
  * Support for 1v1, 2v2, 3v3, 4v4, and FFA matches
  * Auto cam that follows the action
  * Spectator betting system
  * [Elo rating system](https://en.wikipedia.org/wiki/Elo_rating_system)
  * Advanced camera controls
  * In-game store with pets and avatars

Ultimately I was able to implement all of the features. Each one presented its own challenge. One of the most interesting was the Elo rating system. Battle.net does not allow for centralized storage of data for a mod. Instead, the mod can write an encrypted signed file to each player's device. This can hold their own Elo rating and can be adjusted for each match they partake in. A similar mechanism is used for keeping track of credit balances across games.

The biggest challenge during development was the lack of documentation and developer community. At the time there was no official documentation on the editor. My main resources were a few other programmers who communicated through web based forums. The back and forth was slow and there were often times when no one else had tried to tackle some of the problems I was facing.

Much of the code represnts workarounds to default game behavior vs elegant programming solutions. There was a lot of code duplication, for example.

In 2014 another SC2 community member created [GameHeart](https://news.blizzard.com/en-gb/starcraft2/15463641/wcs-gameheart), which took inspiration from existing observer mods, including PeepMode. This mod went on to be used by tournaments and other e-sports competitions while PeepMode continued to be popular as a custom mode on Battle.net.

Lessons learned:
  * Listen to early adopters and implement their common suggestions.
  * Good UI is more important than an impressive feature set.
  * It's hard to recruit talent to passion projects.
  * Someone else will do it better and faster after they see yours. Embrace the competition.
  * Releases are nail-biting without test automation.
  * Good documentation is worth a thousand trials by fire.
