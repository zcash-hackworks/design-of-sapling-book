This document is intended to be a technical overview of [Sapling](https://z.cash/upgrade/sapling.html), a major network upgrade for Zcash which is [slated to activate](https://z.cash/support/schedule.html) in October 2018.

* **This is not a user guide.** If you're a user or business, please refer to the [Sapling Upgrade](https://z.cash/upgrade/sapling.html) documentation instead.
* **This is not a specification.** Please refer to the [Zcash Protocol Specification](https://github.com/zcash/zips/blob/master/protocol/sapling.pdf) and [ZIP243](https://github.com/zcash/zips/blob/master/zip-0243.rst) for a more thorough description of the changes involved in the Sapling upgrade.

------------------------------------------------

# Introduction

Zcash is a cryptocurrency which uses advanced cryptography to provide strong financial privacy to its users. Zcash users send money to and from **payment addresses**. Zcash includes two kinds of payment addresses:

* **Transparent addresses** are similar to the traditional Bitcoin-style addresses. Payments to and from transparent addresses publicly reveal the contents of your transaction, such as the value, origin and destination of funds.
* **Shielded addresses** are payment addresses which use a variant of the [Zerocash protocol](http://zerocash-project.org/) to allow users to keep the value, origin and destination of funds completely private.

Transactions involving only shielded addresses have very strong privacy properties, but transactions that involve both transparent and shielded addresses have complicated privacy properties that are hard to articulate to users. Therefore, it would be nice to eventually remove transparent addresses from the protocol entirely.

The original shielded addresses in Zcash typically require over 40 seconds and more than a gigabyte of memory to send and receive payments with. As a result, transparent addresses are ubiquitous in the ecosystem.

**Sapling** is a Zcash network upgrade that introduces a new shielded address format that is vastly more efficient to send and receive payments with. Slated to activate in October 2018, it will be the product of over two years of cryptographic design, engineering and analysis.
