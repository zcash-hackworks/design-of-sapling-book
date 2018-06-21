# Transaction Design

Transactions in Zcash, just as in Bitcoin, involve inputs and outputs. Transparent outputs contain a value and a predicate for how the value can be spent, and transparent inputs are allowed to spend that value, given they can satisfy the predicate (e.g. with a digital signature). Transparent inputs and outputs have publicly visible value (by their nature) and the consensus rules enforce that the value of the inputs is greater than or equal to the value of the outputs. The residual value is available to the miner as a fee.

We can visualize the flow of value in a transaction through **value pools**. Transparent inputs are adding value to a pool, while transparent outputs are taking value away from it. The consensus rules are effectively forcing this pool to be non-negative.

## Sprout z-addresses

Payments involving Sprout z-addresses revolve around the `JoinSplit` operation. This operation spends two shielded notes (revealing their nullifiers), and creates two new shielded notes (revealing their commitments). The operation ensures that the value of the shielded inputs is equal to the value of the shielded outputs.

Transactions contain a (potentially empty) vector of `JoinSplit` descriptions, each of which contains a zk-SNARK proof, the nullifiers for the inputs, the anchor, and the new note commitments, among other things. In order to allow value to flow between transparent addresses and shielded addresses, each of these `JoinSplit` operations also can interact with the public value pool through `vpub_old` and `vpub_new` fields in the `JoinSplit` description.

In order for `JoinSplit`s to interact with each other in the same transaction (like when you have more than two shielded inputs) the `JoinSplit` descriptions are allowed to use an "interstitial" anchor derived by appending commitments to the tree that a previous `JoinSplit` description used as an anchor. Otherwise, `JoinSplit`s would need to use the (public) value pool of the transaction to move funds around, which would degrade privacy.

Finally, if a transaction contains at least one `JoinSplit` description, there are fields at the end which contain an ephemeral key and signature to prevent malleability. This key is bound to each of the zk-SNARK proofs through a MAC scheme.

## Sapling z-addresses

Sapling's z-addresses have a simpler and more natural interaction with the transaction. Instead of a `JoinSplit` description which involves two shielded inputs and two shielded outputs, transactions contain a vector of `Spend` descriptions and a vector of `Output` descriptions. These correspond to shielded inputs and outputs, respectively.

`Spend` descriptions contain a single nullifier, and `Output` descriptions contain a single note commitment. Each of these descriptions contain their own zk-SNARK proof.

### Value balance

In order to ensure values are balanced between `Spend` and `Output` operations, each description is accompanied by a Pedersen commitment to the value contained in the note being spent or created. The zk-SNARK proof guarantees this commitment is valid. Pedersen commitments are additively homomorphic, and so the outside rules simply sum up the `Spend` value commitments and subtract them from the sum of the `Output` value commitments. The resulting group element should, if the value is balanced, be a group element raised to a *known* uniformly random scalar. The creator of the transaction demonstrates this with a signature.

This is very similar to how Confidential Transactions (CT) works.

In order to allow Sapling z-addresses to interact with other addresses, a signed `vpub` field in the transaction indicates to the consensus rules how much value is being added or subtracted from the public value pool, and the equation involving the Pedersen commitments is modified accordingly.

### Spend authorization

Each `Spend` description contains a key (called `rk`) which is a re-randomization of the spend authorization key `ak` bound to the note being spent. The transaction creator must sign the transaction for this `rk`, and place the signature in the `Spend` description.

### Anchors

`Spend` descriptions must also contain an anchor indicating the Merkle tree that the note is located in. Just as in Sprout `JoinSplit`s, this is required to be an anchor at a previous block boundary. Unlike `JoinSplit`s, there are no interstitial anchors. If the note being spent has a value of zero then the note does not need to exist in the tree at all, allowing users to obfuscate the input arity of their transactions.
