Over time, the Zcash network will undergo **network upgrades** in order to add features and improve the network. We like to use codenames to describe our major releases and network upgrades:

### Sprout

**Sprout** was the initial release of Zcash in 2016. Zcash's protocol is built on top of a fork of Bitcoin's code, with an integration of the Zerocash protocol and some other adjustments:

* The maximum block size was increased to 2MB.
* The interval between blocks targets 2.5 minutes. (Corresponding changes to the block reward ensure that the supply schedule approximates Bitcoin's.)
* The proof-of-work algorithm was changed to Equihash.
* The difficulty adjustment algorithm was modified to react more quickly to changes in hashrate.
* A 32-byte `reserved` field was added to the block header.

### Overwinter

**Overwinter** is Zcash's first network upgrade. Overwinter's main goal is to introduce changes which make future network upgrades simpler. The most important is the introduction of bilateral replay protection: transactions on a different chain that did not follow the network upgrade should not be valid on the new chain, and vice-versa.

Overwinter also had some other changes to consensus rules:

* The quadratic cost of validating (transparent payment) signatures was fixed.
* Transactions now have an expiry height which allows transactions to expire from being mined.

### Sapling

**Sapling** is a major network upgrade that is expected to activate in October 2018. The primary goal of this upgrade is to improve the performance of shielded addresses so that they can become ubiquitous in the ecosystem.

The Sapling upgrade includes:

* A new z-address that is significantly faster to send and receive payments with, with less memory consumption.
* Old z-addresses are still valid, but transactions involving them are doubled in performance.
* Block headers are required to contain (in the previously `reserved` field) the Merkle tree root of the new z-address accumulator.
