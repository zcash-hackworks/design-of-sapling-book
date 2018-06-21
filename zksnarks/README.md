# zk-SNARKs

[Zero-knowledge proofs](https://en.wikipedia.org/wiki/Zero-knowledge_proof) allow you to demonstrate that you performed a computation correctly without revealing all of the inputs to that computation. We can think of the computation as some $$f(x, w)$$, where the **statement** $$x$$ is known to both the verifier and the prover, but the **witness** $$w$$ is known only to the prover.

The fundamental tool underlying Zcash is an advanced zero-knowledge proof called a **zk-SNARK**. These proofs are only hundreds of bytes long and are inexpensive to verify, even if the underlying computation $$f(x, w)$$ is large in complexity. These proofs are also **non-interactive**, so the prover can publish the proof and anyone can verify it without interacting with the prover, making them very useful for cryptocurrencies.

zk-SNARKs do come with some downsides, which are being addressed by the Sapling upgrade:

* zk-SNARKs require a setup phase where, for a given computation $$f(x, w)$$, some **public parameters** are constructed. These parameters are needed to create and verify proofs, but if the creator of the parameters "remembers" how they were constructed, they can create false proofs.
    * Sapling uses a gigantic and public [multi-party computation](https://en.wikipedia.org/wiki/Secure_multi-party_computation) (MPC) ceremony to construct the parameters. In order to corrupt the parameters, a large number of reputable individuals must *all* be colluding in secret or compromised.
* [Pairing-friendly elliptic curves](https://en.wikipedia.org/wiki/Pairing-based_cryptography) are needed, and relatively strong cryptographic assumptions are made.
    * Sapling switches to a more secure and more rigid pairing-friendly elliptic curve.
* The proofs have a reputation for being expensive to create, both in terms of time and memory.
    * Sapling uses a more efficient proving system and novel cryptographic primitives to improve performance. Proving time is reduced by 20x, and memory usage is reduced by orders of magnitude.
