---
title: Nano RPC
excerpt: A Ruby wrapper for controlling Nanocurrency nodes
header:
  image: /assets/images/projects/nano-ruby-rpc-header.jpg
  teaser: /assets/images/projects/nano-ruby-rpc-header.jpg
---

During the 2017 cryptocurrency bull run, I began looking more closely at alternative networks beyond Bitcoin. Of course Ethereum came to the top of that stack, but there were several others that piqued my interest. One of these was [Nano](https://en.wikipedia.org/wiki/Nano_(cryptocurrency)), formerly known as Rai Blocks.

Nano uses a directed acyclic graph approach to handling transactions and uses proof of stake for consensus. These design decisions offer a number of tradeoffs including speed and cost of transactions. Nano transactions work much faster than Bitcoin and are free to conduct for the end user (no miner fees).

Nano was launched in October 2015 by Colin LeMahieu to address the Bitcoin scalability problem and was created with the intention to reduce confirmation times and fees. I found Colin's approach inspiring - it seemed that he was truly out to solve a big problem and was committing a lot of time and effort to it. This inspired me to pitch in some time.

Because I am not an expert in C, I could not contribute directly to the core Nano code, so I looked at other ways of supporting the project. To run a Nano node, an administrator must send RPC commands to it via an HTTP interface. This can be cumbersome to do from the commandline using curl or other linux tools. So I made [a Ruby wrapper](https://github.com/jcraigk/ruby_nano_rpc) so that it was easier to control the servers.

There are two ways to use the Ruby gem. You can use proxy objects that expose helper methods or you make direct RPC calls using Ruby hashes. Here are some examples:

```
# Instantiate an object to interact with a Nano node
node = NanoRpc::Node.new(host: 'mynanonode', port: 1234)

# Call raw RPC commands directly
node.call(:account_balance, account: 'xrb_1234')
# => {"balance"=>100, "pending"=>0}

# Get a wallet and check its balance
NanoRpc.node.wallet('A3B9CF...').balance
# => 1000
```

I went on to experiment with a [cryptocurrency tumbler service](https://en.wikipedia.org/wiki/Cryptocurrency_tumbler) using Nano as the primary network. Technically it was a success but the cost of running a financial service like that legally was beyond my means, so I eventually shelved that project.

The financial value of Nano has gone down considerably since 2017 and it is probably doomed to fail as a currency. However, it continues to prove that alternative approaches to cryptocurrency systems are worth exploring. I enjoyed my time working on this project and interacting with several other talented engineers to build the software.

Lessons learned:
  * There are many different types of people in the crypto space, from benevlent engineers to malevolent financial scammers
  * There are many approaches to solving the various problems posed by crypto systems, each offering a set of tradeoffs for end users
  * The encumbent financial players have safeguards to ensure small players cannot easily compete
  * The world's entire financial system is fragile
