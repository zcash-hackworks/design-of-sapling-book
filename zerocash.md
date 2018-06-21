# Zerocash

Zcash's shielded transactions implement a variant of the [Zerocash protocol](http://zerocash-project.org/). Zcash's implementation differs greatly from the Zerocash paper: we made changes to terminology, fixed some security bugs, and (in the case of Sapling) have begun to make significant modifications for performance.

Shielded transactions still center around three basic principles:

1. **Notes** consist of some value and an address that is allowed to spend it.
2. Cryptographic commitments to all notes that are created are placed in an **accumulator** -- in our case, a Merkle tree. This tree is maintained by all full nodes on the network.
3. In order to spend a note, you reveal a **nullifier** that is bound to the note. The nullifier doesn't reveal which note you are spending. The list of previously revealed nullifiers is maintained by all nodes, and a transaction that attempts to reveal a nullifier twice is rejected as a double-spending transaction.

In order to support large accumulators like deep Merkle trees -- thereby maximizing privacy -- Zerocash relies on advanced zero-knowledge proofs called **zk-SNARKs**. These proofs allow users to spend and create notes while guaranteeing that values are balanced and the revealed nullifiers and commitments are properly computed.

Creating new notes is straightforward: you reveal a note commitment and a proof that the commitment is correctly structured. The value of the new note needs to be compared with the rest of the transaction somehow to ensure that money isn't being created or destroyed.

Spending is a little more complicated. In addition to revealing a nullifier and a proof that it was correctly calculated, you must also prove the note you're spending exists at all, and that you're authorized to spend it. Your proof will witness a path to your note in a merkle tree, and the merkle tree root must be revealed alongside the proof. This root (referred to as an **anchor**) is typically constrained by the outside consensus rules to be some Merkle tree root at a previous block boundary.

Making a payment using this protocol requires some way to send the commitment randomness, value and other information to the recipient, so that they are aware they can spend the note. Zcash uses in-band secret distribution to do this: the address contains an asymmetric key which can be used for a half-ephemeral Diffie-Hellman key exchange, and a ciphertext is placed alongside the new note commitment.

## Important Considerations

Most of the mistakes surrounding concrete instantiations of Zerocash-like protocols involve nullifiers:

1. Nullifiers need to be fully determined by the note. If any of the inputs to the nullifier computation can be substituted at proving time, an adversary could spend the same note multiple times. (One example of this is the [InternalH collision attack](https://blog.z.cash/fixing-zcash-vulns/) discovered by Taylor Hornby.)
2. Nullifiers must be computed [using a PRF](https://en.wikipedia.org/wiki/Pseudorandom_function_family), so that they are indistinguishable from each other.
3. The PRF for computing the nullifier must be keyed on secrets only the spender knows. Otherwise, the original creator of the note can compute the nullifier and see when it is spent.
4. The PRF must also be [collision-resistant](https://en.wikipedia.org/wiki/Collision_resistance). Otherwise, an adversary could create multiple notes with the same nullifier, spending one to ensure the others cannot be spent. This is referred to as a sniping attack.
5. The inputs to the nullifier computation should be unique to each note, so that the final nullifier is different for every note in the tree. This prevents the "Faerie gold attack" (discovered by Zooko Wilcox) which would allow an adversary to send two payments to a recipient, of which only one can be spent.

It's also necessary to defend against malleability attacks where parts of the shielded components of transactions are relocated into other transactions, which would allow for theft. We solve this using digital signatures with ephemeral keys that are bound to the proofs. It is also problematic if the zk-SNARK proofs themselves are malleable; either we must use simulation-extractable proofs, or we must design the construction to mitigate the problem.
