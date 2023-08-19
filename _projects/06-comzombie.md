---
title: ComZombie
excerpt: A financial analysis and trading app focused on the commodities market
header:
  image: /assets/images/projects/comzombie-header.jpg
  teaser: /assets/images/projects/comzombie-header.jpg
---

Early in my programming career (circa 2003), I read [A Random Walk on Wall Street](https://en.wikipedia.org/wiki/A_Random_Walk_Down_Wall_Street). It introduced several interesting concepts about financial trading, chief among them that it was impossible to predict future price moves based on past performance. To test this, I decided to build a financial analysis engine. If the software didn't yield any financial results, at least I would learn a lot while making it.

I started with a PHP app that pulled historical and daily commodities trading data from a subscription brokerage service. It used a browser-based PNG graphing lib to visualize the data. After proving the concept, I rewrote much of the PHP logic in C to improve performance. I added a rudimentary distributed computing framework so I could test as many trading strategies as possible across a set of linux boxes I had setup.

My business partner and I set up a small business called ComZombie to trade the best strategy that the software produced. Ultimately we ended up breaking even after brokerage fees, which were considerable for the frequent trades the system instructed us to execute. Since we both had day jobs we enjoyed, we decided to return our attention there.

While the app did identify a few strategies that may have turned a profit in the longrun (I have not verifed that), ultimately I concluded that the thesis of A Random Walk was correct: it is very difficult, if not impossible, to predict price using statistical analysis alone.

That said, there are many opportunities for small profits based on arbitrage and other well known algorithmic trading strategies. Such systems would probalby have a limited window of use and would likely be kept secret.

Takeaways:
  * C is much faster than PHP at runtime but the development experience is rough
  * The thesis of [A Random Walk on Wall Street](https://en.wikipedia.org/wiki/A_Random_Walk_Down_Wall_Street) seems generally correct
  * It might be best to keep friends and business partners separate
  * It is gratifying and powerful to verify and visualize statistical ideas using software
