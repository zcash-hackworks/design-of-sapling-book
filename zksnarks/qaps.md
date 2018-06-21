# Quadratic Arithmetic Programs (QAPs)

## QAPs from R1CS

One way to prove that we know a satisfying assignment to some rank-1 constraint system is to actually reveal our assignment $$\textbf{z}$$ to the verifier. The verifier can check that $$\langle \textbf{a}_i, \textbf{z} \rangle \cdot \langle \textbf{b}_i, \textbf{z} \rangle = \langle \textbf{c}_i, \textbf{z} \rangle$$ holds for all $$i$$. However, this isn't zero-knowledge, nor does it lead to short proofs.

Our first goal is to compress the $$i$$ different inner product equations into a *single* equation. We do this through the use of [interpolation polynomials](https://en.wikipedia.org/wiki/Polynomial_interpolation). Let $$u_i(x)$$ be a polynomial that interpolates over all of the $$i$$th elements in $$\textbf{a}$$ at $$k$$ distinct points $$r_0, r_1, ..., r_{k-1}$$. Do the same for $$v_i(x)$$ with $$\textbf{b}$$ and $$w_i(x)$$ with $$\textbf{c}$$.

We can now express our constraint system in a single equation:

$$
\langle \textbf{u(x)}, \textbf{z} \rangle \cdot \langle \textbf{v(x)}, \textbf{z} \rangle = \langle \textbf{w(x)}, \textbf{z} \rangle
$$

If we evaluate this equation at the point $$x = r_i$$, the vectors of interpolation polynomials will evaluate into vectors of coefficients that correspond to the $$i$$th constraint. This means that although we have simplified the condition into a single equation, we still have to check that the equation is satisfied at $$k$$ different points.

Let's rearrange the equation slightly by setting the right hand side to zero:

$$
\langle \textbf{u(x)}, \textbf{z} \rangle \cdot \langle \textbf{v(x)}, \textbf{z} \rangle - \langle \textbf{w(x)}, \textbf{z} \rangle = 0
$$

It is possible for us to check that this equation holds at each of the points $$r_0, r_1, ..., r_{k-1}$$ by constructing a **target polynomial** $$t(x) = \prod_{i=0}^{k-1} (x - r_i)$$ which has roots at each point. It turns out that if $$\langle \textbf{u(x)}, \textbf{z} \rangle \cdot \langle \textbf{v(x)}, \textbf{z} \rangle - \langle \textbf{w(x)}, \textbf{z} \rangle$$ really is zero at each point, then $$t(x)$$ will divide it. Let's call the $$k - 2$$ degree quotient polynomial $$h(x)$$.

The prover now gives the verifier the assignment $$\textbf{z}$$ and the coefficients $$\textbf{h}$$ of the $$h(x)$$ polynomial, and the verifier can [probabilistically check](https://en.wikipedia.org/wiki/Schwartz%E2%80%93Zippel_lemma) that the constraint system is satisfied by choosing a random $$x \in \mathbb{F}_q$$ and checking that the following equation holds:

$$
\langle \textbf{u(x)}, \textbf{z} \rangle \cdot \langle \textbf{v(x)}, \textbf{z} \rangle - \langle \textbf{w(x)}, \textbf{z} \rangle = \langle \textbf{x}^{k-1}, \textbf{h} \rangle \cdot t(x)
$$

We call this relation a quadratic arithmetic program or QAP for short.
