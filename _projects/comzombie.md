---
title: ComZombie
excerpt: A financial analysis and trading app focused on the commodities market
header:
  image: /assets/images/projects/comzombie-logo-wide.png
  teaser: /assets/images/projects/comzombie-logo-wide.png
---

Early in my programming career, I read [A Random Walk on Wall Street](https://en.wikipedia.org/wiki/A_Random_Walk_Down_Wall_Street). It introduced several interesting concepts about financial trading, chief among them that it was impossible to predict future price moves based on past performance. To test this, I decided to build a financial analysis app. If the app didn't yield any financial results, at least I would learn a lot while making it.

I started with a PHP app that pulled historical and daily commodies trading data from a brokerage I subscribed to. I used a graphing program in the browser to visualize the data. For performance, much of the PHP logic was rewritten in C. I added a rudimentary distribute computing framework to test trading strategies across multiple nodes.

My business partner and I set up a small business called ComZombie to trade the best strategy that the software produced. Ultimately we ended up breaking even after brokerage fees, which were considerable. Sinc we both had day jobs we enjoyed, we decided to shutter the business and the software.

While the app did identify a few strategies that may have turned a profit in the longrun (I have not verifed that), ultimately I concluded that the thesis of A Random Walk was correct: it is very difficult, if not impossible, to predict price using statistical analysis alone.

That said, I would not be surprised if other smarter people have created just that, especially in today's crypto market. Such systems would probalby have a limited window of use and would be kept secret.

Takeaways:
  * C is much faster than PHP at runtime but the development experience is rough
  * The thesis of [A Random Walk on Wall Street](https://en.wikipedia.org/wiki/A_Random_Walk_Down_Wall_Street) is probably correct
  * It is often best to compartmentalize friends and business partners
  * It is gratifying and powerful to verify ideas using software
