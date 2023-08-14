---
title: StoryKey
excerpt: An experimental brainwallet
header:
  image: /assets/images/projects/storykey-wide.png
  teaser: /assets/images/projects/storykey-wide.png
---

[StoryKey](https://github.com/jcraigk/storykey) is a proof of concept [Brainwallet](https://en.bitcoin.it/wiki/Brainwallet) inspired by [BIP39](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki) written in Ruby. It converts an arbitrary string of data, such as a [cryptocurrency private key](https://en.bitcoin.it/wiki/Private_key), into an English paragraph intended for longterm human memory. It also assists in decoding the story back into its original form. Optionally, a visual representation of the paragraph is also provided using [OpenAI DALL-E](https://openai.com/dall-e-2).

![CLI](https://user-images.githubusercontent.com/104095/210197560-45494c50-6382-465b-8163-a61b3783ac76.png)

![Dalle](https://user-images.githubusercontent.com/104095/210197577-11e1d6ac-a32f-4438-b7eb-f766bf62f0f2.png)

I picked up a [Ledger Nano](https://shop.ledger.com/pages/ledger-nano-x) to take control of my own crypto keys. This hardware wallet uses an initial private seed to generate identities for many common cryptocurrencies. The private seed is recoverable from a seed phrase, which consists of 24 words that the user must memorize and keep private. This enables recovery of all derivative identities, and therefore funds, in case of hardware loss or failure. I found the process of memorizing these words to be challenging. The lexicon is somewhat random, with different parts of speech mixed in randomly.

I theorized that the phrase might be easier to remember if it used different parts of speech grammatically to form images in one's mind. These images could then be visually presented as a mnemonic device along with the text. Perhaps some people may find remembering the images easier than the text, or vice versa.

It would take some kind of survey or test administered to actual end users to find out if the software produces any change in mnemonic properties. I may try to conduct that at some point, but for now I will continue to tinker with the idea. Image generation AI's continue to improve, and an important next step will be using more detailed prompts to produce consistent memorable imagery. I may also be able to use large language models to produce better lexicons or even culturally specific lexicons.

Takeaways
  * It is difficult to produce lexicons appropriate for the widest audience - cultural references are useful but not universal
  * Stable diffusion image generation currently (2023) produces a lot of randomness
  * It is unclear whether structured phrases are easier to memorize than random words
