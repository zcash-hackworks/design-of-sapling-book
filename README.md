This document is intended to be a technical overview of [Sapling](https://z.cash/upgrade/sapling.html), a major network upgrade for Zcash which is [slated to activate](https://z.cash/support/schedule.html) in October 2018.

* **This is not a user guide.** If you're a user or business, please refer to the [Sapling Upgrade](https://z.cash/upgrade/sapling.html) documentation instead.
* **This is not a specification.** Please refer to the [Zcash Protocol Specification](https://github.com/zcash/zips/blob/master/protocol/sapling.pdf) and [ZIP243](https://github.com/zcash/zips/blob/master/zip-0243.rst) for a more thorough description of the changes involved in the Sapling upgrade.

------------------------------------------------

# Introduction

This document is an attempt to describe the cryptography underpinning Zcash's upcoming Sapling network upgrade with extraordinary detail, both for public education and for auditors of the system's security. We start with abstract concepts and cryptographic tools, and then visit the higher level protocol details.

### What is Sapling?

Zcash is a cryptocurrency which uses advanced cryptography to provide strong financial privacy to its users. Zcash users send money to and from **payment addresses**. Zcash includes two kinds of payment addresses:

* **Transparent addresses** are similar to the traditional Bitcoin-style addresses. Payments to and from transparent addresses publicly reveal the contents of your transaction, such as the value, origin and destination of funds.
* **Shielded addresses** are payment addresses which use a variant of the [Zerocash protocol](http://zerocash-project.org/) to allow users to keep the value, origin and destination of funds completely private.

Transactions involving only shielded addresses have very strong privacy properties, but transactions that involve both transparent and shielded addresses have complicated privacy properties that are hard to articulate to users. Therefore, it would be nice to eventually remove transparent addresses from the protocol entirely.

The original shielded addresses in Zcash typically require over 40 seconds and more than a gigabyte of memory to send payments with. As a result, transparent addresses are ubiquitous in the ecosystem.

**Sapling** is a Zcash network upgrade that introduces a new shielded address format that is vastly more efficient to send and receive payments with. Slated to activate in October 2018, it will be the product of over two years of cryptographic design, engineering and analysis.

### Who is behind Sapling?

Sapling's design is based heavily on the Zerocash protocol, designed by [seven scientists](https://z.cash/team.html#scientists) who helped found the Zcash Company. Sapling improves on Zerocash with numerous design changes and optimizations by Zcash engineer Sean Bowe, and Zcash scientists Matthew Green and Ian Miers. Numerous clever optimizations and design improvements were devised by Daira Hopwood. Daira Hopwood is also primarily responsible for the thorough protocol specification.

Much of the optimization and design work of Sapling took place publicly on our [Github issue tracker](https://github.com/zcash/zcash/issues). In these discussions you can see our attempted optimizations, dead ends, and the potential mistakes we discovered along the way. Check out [#2277](https://github.com/zcash/zcash/issues/2277), [#2234](https://github.com/zcash/zcash/issues/2234), [#2247](https://github.com/zcash/zcash/issues/2247), and [#2233](https://github.com/zcash/zcash/issues/2233) if you're interested.

Many others helped advise and review the cryptography underlying Zcash, both at the Zcash Company and in the broader academic community; check the acknowledgements in our [protocol specification](https://github.com/zcash/zips/blob/master/protocol/sapling.pdf) for more information about these awesome people. The Zcash company has also [solicited audits](https://blog.z.cash/2018-security-audits/) of the cryptography and code.
