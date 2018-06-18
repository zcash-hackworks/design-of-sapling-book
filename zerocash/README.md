# Zerocash

Zcash's shielded transactions implement a variant of the Zerocash protocol. Although we made some changes to terminology and fixed some security bugs, the construction still centers around three basic principles:

1. **Notes** consist of some value and an address that is allowed to spend it.
2. Cryptographic commitments to all notes that are created are placed in an **accumulator** -- in our case, a Merkle tree. This tree is maintained by all full nodes on the network.
3. In order to spend a note, you reveal a **nullifier** that is bound to the note. The nullifier doesn't reveal which note you are spending. The list of previously revealed nullifiers is maintained by all nodes, and a transaction that attempts to reveal a nullifier twice is rejected as a double-spending transaction.

In order to support large accumulators like deep Merkle trees -- thereby maximizing privacy -- Zerocash relies on advanced zero-knowledge proofs called **zk-SNARKs**.
