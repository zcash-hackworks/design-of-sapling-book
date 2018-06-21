# Groth16

QAPs allow us to demonstrate that a statement is true with a single identity test:

$$
\langle \textbf{u(x)}, \textbf{z} \rangle \cdot \langle \textbf{v(x)}, \textbf{z} \rangle - \langle \textbf{w(x)}, \textbf{z} \rangle = \langle \textbf{x}^{k-1}, \textbf{h} \rangle \cdot t(x)
$$

In order to achieve zero-knowledge and short proofs, we need the prover to calculate the inner products and send the results to the verifier. However, the prover cannot know the point $$x$$ at which the QAP will be evaluated, or they will be able to find $$h(x)$$ for which the identity holds for any statement.
