---
title: Phish.in
excerpt: An open source website and API of live Phish audience recordings
header:
  image: /assets/images/projects/phishin-header.jpg
  teaser: /assets/images/projects/phishin-header.jpg
---

I discovered Phish in 1994 playing basketball with my brother. HORSE was our game. We'd play on our blacktop driveway in rural upstate NY while listening to CDs on a Sony boombox. One day my brother brought home [Rift](https://en.wikipedia.org/wiki/Rift_(album)). I wasn't serious about playing keyboards at the time but I was interested in that instrument in general probably because my father played. When I heard [Page McConnell](https://en.wikipedia.org/wiki/Page_McConnell) play piano and B3 on that album, I was amazed. The piano could sound like _that_? Wow.

It was soon after that I discovered how prolific the band was with their live performances, all of which were different. There were costumes (musical and otherwise), secret languages, vacuum cleaner solos, a [fantasy epic](https://en.wikipedia.org/wiki/Gamehendge), and extended improvisation ("jamming"). Also a bunch of weird drugged out brilliant people who followed them around.

Phish allows the audience to [record and trade](https://phish.com/faq/#:~:text=Audience%20taping%20at%20Phish%20concerts,the%20exclusive%20property%20of%20Phish.) their shows as long as no money or promotion is involved. In the nineties, the only way to hear live shows was by trading cassettes with other fans. There was a head shop in Rochester, NY that I would visit whenever I could get someone to drive me (I was 14 at the time). They had a book listing all their Dead and Phish tapes. If you left a cassette they would make you a copy for free. This was how my tape collection grew to about 50 tapes. The era of mp3s soon took over, at which point I stopped adding to my collection.

In 2010 I was at a Phish show discussing tape trading and other ideas with a fellow software engineer. He mentioned he had begun work on an idea we (and many others) had - a website that hosted Phish audience recordings in mp3 format. At the time, the best we had was the "Phish Spreadsheet", which was a Google spreadsheet of dates linked to Flacs hosted on low end file sharing sites like Mediafire.

My colleague's vision was to have a simple mobile app where you could quickly navigate and play tracks. My vision was a bit different in that I wanted a desktop version that had a lot of bells and whistles.

We started by creating [PhishTracks](https://www.phishtracks.com/), importing audio from the Spreadsheet. We released the site in 2012. I then forked that into [Phish.in](https://phish.in/) to complete the vision I had individually. True to our original visions, the former works great on mobile while the latter provides more features in a desktop setting. Phish.in also provides an [API](https://phish.in/api-docs) which powers apps such as [Relisten](https://apps.apple.com/us/app/relisten-all-live-music/id715886886).

Over the last ten years I've continued to add features to the site and curate the recordings provided by generous community tapers. To cite a cliche, it's been a labor of love. I am very lucky to have found this community and this will likely be a lifelong project for me.

Takeaways:
  * [Dokku](https://dokku.com/) is great for hosting single server apps
  * [Cloudflare](https://www.cloudflare.com/) provides excellent free caching for web app content
  * [bt.etree.org](https://bt.etree.org/) is a great service for live music fans
  * Phish concert tapers are dedicated to their craft
  * If you build it, they will come
