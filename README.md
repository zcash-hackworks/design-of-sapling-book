This document is intended to be a technical overview of [Sapling](https://z.cash/upgrade/sapling.html), a major network upgrade for Zcash which is [slated to activate](https://z.cash/support/schedule.html) in November 2018.

* **This is not a user guide.** If you're a user or business, please refer to the [Sapling Upgrade](https://z.cash/upgrade/sapling.html) documentation instead.
* **This is not a specification.** Please refer to the [Zcash Protocol Specification](https://github.com/zcash/zips/blob/master/protocol/sapling.pdf) and [ZIP243](https://github.com/zcash/zips/blob/master/zip-0243.rst) for a more thorough description of the changes involved in the Sapling upgrade.

------------------------------------------------

# Introduction

Zcash is a cryptocurrency which uses cutting-edge cryptography to provide users with strong privacy guarantees. Over time, the Zcash network will undergo **network upgrades** in order to add features and improve the network. We like to use codenames to describe our major releases and network upgrades:

### Sprout

**Sprout** was the initial release of Zcash in 2016. Zcash's protocol is built on top of a fork of Bitcoin's code. Just as in Bitcoin, users typically send and receive money with **payment addresses**. The original release of Zcash included two kinds of payment addresses:

* **Transparent addresses** are identical to the traditional Bitcoin-style addresses. Payments to and from transparent addresses publicly reveal the contents of your transaction, such as the value, origin and destination of funds.
* **Shielded addresses** are payment addresses which use a variant of the [Zerocash protocol](http://zerocash-project.org/) to allow users to keep the value, origin and destination of funds completely private.

### Overwinter

**Overwinter** is Zcash's first network upgrade. It makes some changes to the protocol which make future network upgrades simpler. It is slated to activate in June 2018.

### Sapling

**Sapling** is a major network upgrade that is expected to activate in November 2018. The primary goal of this upgrade is to improve the performance of shielded addresses so that they can become ubiquitous in the ecosystem. In order to do this, we need to make payments involving these addresses much more efficient. This requires using some improved cryptographic tools and a new kind of shielded address.

Sapling is one step toward removing transparent addresses from the protocol entirely, although that will not take place in the Sapling upgrade.
