This document is intended to be a technical overview of [Sapling](https://z.cash/upgrade/sapling.html), a major network upgrade for Zcash which is [slated to activate](https://z.cash/support/schedule.html) in October 2018.

* **This is not a user guide.** If you're a user or business, please refer to the [Sapling Upgrade](https://z.cash/upgrade/sapling.html) documentation instead.
* **This is not a specification.** Please refer to the [Zcash Protocol Specification](https://github.com/zcash/zips/blob/master/protocol/sapling.pdf) and [ZIP243](https://github.com/zcash/zips/blob/master/zip-0243.rst) for a more thorough description of the changes involved in the Sapling upgrade.

------------------------------------------------

# Background

Zcash is a cryptocurrency which uses cutting-edge cryptography to provide users with strong financial privacy. Zcash users send money to and from **payment addresses**. Zcash includes two kinds of payment addresses:

* **Transparent addresses** are similar to the traditional Bitcoin-style addresses. Payments to and from transparent addresses publicly reveal the contents of your transaction, such as the value, origin and destination of funds. There is a `t` at the beginning of all transparent addresses, so we sometimes call them "t-addresses."
* **Shielded addresses** are payment addresses which use a variant of the [Zerocash protocol](http://zerocash-project.org/) to allow users to keep the value, origin and destination of funds completely private. There is a `z` at the beginning of all shielded addresses, so we sometimes call them "z-addresses."

**Sapling** is a [network upgrade](background/network_upgrades.md) which introduces a new z-address which is faster to send and receive shielded payments with. It is the first step toward (eventually) removing transparent addresses from Zcash completely.

The Sapling network upgrade has required more than a year of careful design and optimization. This document is intended to give a technical and cryptographic overview of the Sapling upgrade so that it can be more broadly analyzed by the community.
