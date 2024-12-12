---
title: Phish.in
excerpt: An open source website and API of live Phish audience recordings
header:
  image: /assets/images/projects/phishin-header.jpg
  teaser: /assets/images/projects/phishin-header.jpg
---

Music and community are closely related in human culture. In modern times, we enjoy instant access to millions of artists and their work through services like Spotify. This, of course, was not the case even just a few years ago. Before modern recording was invented, enjoying music required either creating it yourself or listening to others play. And even after that but before the ubiquity of the Internet, listening to music required a playback device like a record player or walkman. As someone who grew up in the nineties, listening to tapes and CDs communally was commonplace, and concerts were an important social experience.

My first love of music was [Trent Reznor](https://en.wikipedia.org/wiki/Trent_Reznor)'s work in Nine Inch Nails. The album Closer, which still holds up pretty well, was one of my favorite pieces of music to listen to as a young teen. It seemed to capture the angst I was feeling at the time, and I enjoyed playing it loudly as a kind of protest to other forms of music I found to be too...delicate. As my tastes evolved and my interest in music theory began to bud, I branched out into other forms of rock as well as jazz and hiphop. I enjoyed discovering new artists who combined these elements in unique ways.

![Rift album cover by Dave Welker](/assets/images/projects/phishin/rift-dave-welker.jpg){:.image-centered}
Cover of the Phish album "Rift" by Dave Welker
{:.caption}

In the summer of 1994, at age 13, I was playing basketball with my elder brother when I first heard the improvisational rock band Phish. We would often play compact discs on a Sony boombox while we squared up against each other. The album was [Rift](https://en.wikipedia.org/wiki/Rift_(album)), their fourth studio release. It features several of their now iconic songs, including "Maze" and "My Friend, My Friend." The four members of the band displayed amazing virtuosity as they played their often whimsical but progressive sounding tunes, and it piqued my interest.

I wasn't serious about playing keyboards at the time but I was interested in that instrument in general probably because my father played classical pieces as a hobby on his baby grand. When I heard [Page McConnell](https://en.wikipedia.org/wiki/Page_McConnell) play piano, Hammond B3 organ, and clavinet on that album, I was amazed. Keyboards could sound like _that?_ Wow.

It was soon after that I discovered how prolific the band was with their live performances, all of which featured unique setlists and performative elements. Their concerts ("shows") feature costumes (musical and sometimes physical), secret languages, vacuum cleaner solos, a [fantasy epic](https://en.wikipedia.org/wiki/Gamehendge), a dazzling light show, as well as extended improvisation ("jamming"). Their community consisted of a herd of weird drugged out brilliant people who followed them around. I was intrigued!

![Indoor Phish concert photo](/assets/images/projects/phishin/concert-photo-1.jpg){:.image-centered}
Photo of a live indoor Phish concert (snapped by me)
{:.caption}

Similar to their predecessors the [Grateful Dead](https://en.wikipedia.org/wiki/Grateful_Dead), Phish allows the audience to [record and trade](https://phish.com/faq/#:~:text=Audience%20taping%20at%20Phish%20concerts,the%20exclusive%20property%20of%20Phish.) their shows as long as no money or promotion is involved. In the 1990s, the only way to hear live shows was by physically attending or trading cassettes with other fans. There was a head shop in Rochester, NY that I would visit whenever I could get someone to drive me from our rural farm in the Finger Lakes. The shop provided a book that listed all the Dead and Phish tapes that the proprietor had collected. If you left a cassette, he would make you a copy for free. This was how my tape collection grew to about 50 tapes over the course of a year or two. As the late nineties rolled around, the era of mp3s soon took over, at which point I stopped adding to my collection and turned to file sharing apps like Napster to expand my collection. I also began attending the shows near me, which was a transformative experience for me.

![Outdoor Phish concert photo](/assets/images/projects/phishin/concert-photo-2.jpg){:.image-centered}
Photo of a live outdoor Phish concert (snapped by me)
{:.caption}

In 2010 I was at a Phish show discussing tape trading and other ideas with a fellow software engineer. He mentioned he had already begun work on an idea we (and many others) had considered for a long time - a website that hosted Phish audience recordings in MP3 format. At the time, the best we had was the "Phish Spreadsheet", which was a Google spreadsheet of dates linked to lossless audio files (FLAC format) hosted on low end file sharing sites like MediaFire.

My friend's vision was to have a simple mobile app where fans could quickly navigate and play tracks from any taped show in history. My vision was a bit different in that I wanted a desktop version that had a lot of bells and whistles, including an API for others to access. However, there was a large overlap in our visions so we began working together to realize the initial site.

We started by creating [PhishTracks](https://www.phishtracks.com/) using the Ruby on Rails web development framework. We imported audio from the Spreadsheet, converting the FLACs to MP3s and using a Postgres database to handle the metadata. We released the site in 2012 and it quickly became ubiquitous among the Phish community as a way to listen to past shows for free. I then forked that into [Phish.in](https://phish.in/) to complete the vision I had developed individually. A few years later, I [open sourced](https://github.com/jcraigk/phishin) the project. True to our original visions, the former works great on mobile while the latter provides more features in a desktop setting. Phish.in also provides an [API](https://phish.in/api-docs) which powers apps such as [Relisten](https://relisten.net), also an [open source project](https://github.com/relistennet).

![Phishin Eras screenshot](/assets/images/projects/phishin/eras.jpg){:.image-centered}
Screenshot of the Phish.in landing page, featuring years split by era
{:.caption}

Over the last decade I've continued to add features to the site and curate the recordings provided by generous community tapers. To cite a cliché, it's been a labor of love. I am very lucky to have found this community and am happy to dedicate some of my spare time to this lifelong project. I hope it will continue after I'm gone.

In 2024, I overhauled the site by adding a more complete API and a frontend written in [React](https://en.wikipedia.org/wiki/React_(software)). I also used generative AI to create album covers for each of the shows. While the API still powers the Relisten app, the site now works well on mobile devices as it does on desktop.

![Phishin Show and Player screenshot](/assets/images/projects/phishin/show-and-player.jpg){:.image-centered}
Screenshot of a Phish.in concert page including integrated audio player
{:.caption}

As of December 2024, the site has over 100,000 monthly active users, including web and native apps. My plan is to continue to develop the site so that eventually it will feature lossless audio and multiple sources (tapes) per show. Hopefully advancements in AI will make this much easier in the coming years.

**Takeaways:**
  * [Dokku](https://dokku.com/) is great for hosting single server apps
  * [Cloudflare](https://www.cloudflare.com/) provides excellent free caching for web app content
  * [bt.etree.org](https://bt.etree.org/) is a great service for live music fans
  * Phish concert tapers are dedicated to their craft
  * If you build a valuable community resource, it will get used!
