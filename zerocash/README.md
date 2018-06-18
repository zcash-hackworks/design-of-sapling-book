# Zerocash

Zcash's shielded transactions implement a variant of the Zerocash protocol. Although we made some changes to terminology and fixed some security bugs, the construction centers around three basic principles:

1. **Notes** consist of some value and an address that is allowed to spend it.
2. Cryptographic commitments to all notes that are created are placed in an **accumulator** -- in our case, a Merkle tree. This tree is maintained by all full nodes on the network.
3. In order to spend a note, you reveal a **nullifier** that is bound to the note. The nullifier doesn't reveal which note you are spending. The list of previously revealed nullifiers is maintained by all nodes, and a transaction that attempts to reveal a nullifier twice is rejected as a double-spending transaction.

These are some of the basic principles underlying many private cryptocurrency protocols, including Cryptonote. However, Zcash's shielded transactions use advanced zero-knowledge proofs called **zk-SNARKs**. These proofs allow us to use a large accumulator rather than ring signatures, which scale poorly to large anonymity sets.

