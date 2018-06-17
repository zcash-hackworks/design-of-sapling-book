# Shielded Transactions

Zcash's protocol is built on top of a fork of Bitcoin's code, and so much of the functionality of Bitcoin is still available to users. Users typically send and receive funds between **addresses**. Bitcoin-style addresses in Zcash are called **transparent addresses** as their transaction contents (such as the value, source and destination of funds) are published on the blockchain. These transparent addresses rely on the same mechanisms that Bitcoin uses: a UTXO model, and authorization using ECDSA signatures.

Zcash also includes **shielded addresses**. Payments to and from shielded addresses are kept completely private using a variant of the [Zerocash protocol](http), and so all of the aforementioned properties are kept hidden. It [gets messy](http) when payments involve both transparent and shielded addresses, but transactions involving only shielded addresses have incredibly strong privacy guarantees.

One of the goals of the Sapling network upgrade is to make shielded addresses ubiquitous, which would allow us to remove transparent addresses from the protocol entirely. In order to do this, we need to make payments involving these addresses much more efficient. This requires the design of a new form of shielded address.

## Notes



1. Money is stored in **notes**. Notes represent some value and (currently) an address that represents who owns the money and is exclusively allowed to spend it.
