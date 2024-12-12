---
title: GigTablet
excerpt: An app for gigging musicians to organize songs and manage setlists
header:
  image: /assets/images/projects/gigtablet-header.jpg
  teaser: /assets/images/projects/gigtablet-header.jpg
---

One of my primary hobbies is playing piano and other keyboards in rock, funk, and jazz bands. My brain readily retains math and programming languages but struggles to memorize chord progressions and note sequences, strangely. To accommodate this limitation, for several years I used [MainStage](https://en.wikipedia.org/wiki/MainStage_(software)) to help me with my gigging repertoire. On the left I kept a simple setlist of songs and on the right were the notes for each one. Unfortunately at the time it had no phone/tablet UI so without mobile support I was tied to my laptop during gigs. It was a hassle to bring my laptop to every gig and from an audience perspective, it looked rather clunky.

![GigTablet screenshot](/assets/images/projects/gigtablet/mainstage.jpg){:.image-centered}
MainStage running on my laptop circa 2015
{:.caption}

I noticed that other musicians at the time were using Google Docs to store their song charts, which they could load on any device. They would setup tables of contents to jump to specific songs and use a text-based approach for chords and lyrics. This setup is adequate for most gigs, but it's cumbersome and limiting in several ways. While Google Docs is multi-user, it was not always the best idea to give edit access to other musicians who might mess up your charts. Giving read-only access meant other musicians would copy it and make their own changes. This kind of distributed model works well for software, but I found it wasn't as good for sharing musical notes.

To solve these issues, I built [GigTablet](https://gigtablet.com), a simple progressive web app (WPA) written in [Ruby on Rails](https://rubyonrails.org/). It has a simple UI that lets groups of artists share a repertoire, manage their own notes, build setlists, and stay coordinated during live performance.

![GigTablet screenshot](/assets/images/projects/gigtablet/screenshot-1.jpg){:.image-centered}
Song list view with filtering and quick search
{:.caption}

I've been refining the app while gigging in the soul funk band [OC Funk Collective](/projects/oc-funk-collective). The horn players have been able to eliminate a lot of paper rustling on stage and I've reduced physical and visual clutter by moving from a laptop to a tablet or even my phone in a pinch. One downside is that the musical scores are not editable - the app uses the [Trix](https://trix-editor.org) rich text editor, which supports minimal text styling and images. The horn players score out the lines in [MuseScore](https://musescore.org/en) and take screenshots to paste into GigTablet. Eventually I'd like to support more advanced charting functionality, similar to the popular [iReal Pro](https://www.irealpro.com) app while retaining the multi-user permission system, which these other apps lack.

![GigTablet screenshot](/assets/images/projects/gigtablet/screenshot-2.jpg){:.image-centered}
GigTablet performance mode featuring split view
{:.caption}

I used to think that keeping notes on stage signaled a lack of preparation, but as devices and teleprompters have become standard equipment for professional performers, that mindset has evolved. Today, my tablet serves as a reliable safety net, bolstering confidence even when faced with rarely-played songs from our extensive repertoire. This solution gives me precise control that commercial alternatives can't match, even if it does mean additional work between gigs.

Takeaways:
  * All the available music/gigging apps have their strengths and weaknesses
  * Getting a seven piece band to coordinate is like herding cats
  * You can't expect horn players to scan their own documents
