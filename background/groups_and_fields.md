# Groups and Fields

Much of the cryptography underpinning Zcash depends on algebraic structures with certain properties. <a href="https://en.wikipedia.org/wiki/Group_(mathematics)">Groups</a> and <a href="https://en.wikipedia.org/wiki/Field_(mathematics)">Fields</a> are two of these structures. There is a wealth of resources for learning about these structures on the Internet, but this document will provide an overview of the details which are relevant for Zcash.

## Groups

We refer to a **group** $$\mathbb{G}$$ as a set of elements $$\textbf{S}$$ together with a binary operation $$+$$ defined over those elements. We usually write group elements $$A \in \mathbb{G}$$ with an uppercase letter. In order to be considered a group, several properties (the "group axioms") must hold:

* **Closure**: The operation $$+$$ must always produce another element of the group.
* **Associativity**: Given any $$A, B, C \in \mathbb{G}$$, it must be that $$(A + B) + C = A + (B + C)$$.
* There must be an **additive identity** element $$0$$ for which $$0 + A = A + 0 = A$$ for all $$A \in \mathbb{G}$$.
* Any element $$A$$ must have an **additive inverse** $$B$$ such that $$A + B = 0$$. We usually call $$B = -A$$ the "negative" of the element.

We often deal with "abelian" groups for which the following property also holds:

* **Commutativity**: Given any $$A, B \in \mathbb{G}$$, it must be that $$A + B = B + A$$. In other words, the order of the operations doesn't generally matter, which is stronger than what is implied by the associativity property.

The simplest example of a group is the integers $$\mathbb{Z}$$ under addition, which has an infinite number of elements. In cryptographic contexts, we typically work with groups with a finite number of elements. We refer to the number of elements in a group as its **order**.

Consider the finite group $$\mathbb{Z}_m$$, which is defined as the integers $$\mathbb{Z}$$ [modulo](https://en.wikipedia.org/wiki/Modulo_operation) some integer $$m > 0$$ under addition. In this group, the set $$\textbf{S}$$ is the set of integers $$\{0, 1, 2, ..., m - 1\}$$, and $$A + B$$ is the "remainder" of the division by $$m$$ of the result. As an example, consider the group $$\mathbb{Z}_{12}$$ where $$12$$ corresponds to the number of hours on a wall clock. In this group, $$5 + 10 = 3$$; it is a "cyclic" group for which the addition operator "wraps around" the hours on a clock.

We cannot "multiply" group elements together, but we can "scale" them by adding them to themselves some number of times. As an example, we can scale a group element $$G$$ by $$3$$ by computing $$G + G + G$$. Generally, if an element $$G \in \mathbb{G}$$ is scaled by a **scalar** $$s$$, we write it as $$[s] G$$. We usually write scalars in lowercase letters.

If a group element $$G \in \mathbb{G}$$ can be scaled to produce any other element in the group, we say that it is a **generator** of $$\mathbb{G}$$. If the group is of composite order, some elements will generate a smaller "subgroup" of the original group with order that is some factor of the original order. If the group is prime order, all nonzero elements generate the entire group. Group elements themselves have an "order" described as the number of elements they can generate through scalar multiplication.

## Fields

We refer to a **field** $$\mathbb{F}$$ as a set of elements $$\textbf{S}$$ together with two binary operators $$+$$ and $$*$$ for which the following applies:

* **Closure**: The operations $$+$$ and $$*$$ must always produce another element of the field.
* **Associativity**: Given any $$a, b, c \in \mathbb{G}$$, it must be that $$(a + b) + c = a + (b + c)$$ and it must be that $$(a * b) * c = a * (b * c)$$.
* **Commutativity**: Given any $$a, b \in \mathbb{G}$$, it must be that $$a + b = b + a$$ and it must be that $$a * b = b * a$$.
* **Distributivity**: Multiplication "distributes" over addition such that $$a * (b + c) = (a * b) + (a * c)$$ for all $$a, b, c \in \mathbb{F}$$.
* There must be an **additive identity** element $$0$$ for which $$0 + a = a + 0 = a$$ for all $$a$$.
* There must be an **multiplicative identity** element $$1$$ for which $$1 * a = a * 1 = a$$ for all $$a$$.
* Any element $$a$$ must have an **additive inverse** $$b$$ such that $$a + b = 0$$. We usually call $$b$$ the "negative" of the element.
* Any element $$a \neq 0$$ must have a unique **multiplicative inverse** $$b$$ such that $$a * b = 1$$. We sometimes call $$b$$ the "reciprocal" of the element. Usually we just refer to this as the "inverse" if the context is clear.

The most common example of a field is the real numbers $$\mathbb{R}$$ which contains an infinite number of elements. In fields, polynomials and other kinds of common arithmetic are all usable and have consistent properties. In cryptography we tend to work with fields with a finite number of elements for precision and space-efficiency reasons.

The easiest way to construct a finite field is to select some prime $$p$$ and treat $$Z_p$$ as a field under addition and multiplication modulo $$p$$. All of the above properties apply so long as $$p$$ is prime. All finite fields have $$p^k$$ elements for some prime $$p$$ and some **degree** $$k > 0 \in \mathbb{Z}$$. We call $$p$$ the **characteristic** of the field and typically write such fields as $$\mathbb{F}_{p^k}$$.

Importantly, if we have an abelian group $$\mathbb{G}$$ of prime order $$p$$, then the scalars for any $$G \in \mathbb{G}$$ are elements of $$\mathbb{F}_p$$.

### Field extensions

It is also possible to "extend" a field, much like how the complex numbers $$\mathbb{C}$$ are an extension of the real numbers. All field extensions are themselves fields.

We describe $$\mathbb{C}$$ formally as $$\mathbb{R}[x] / (x^2 + 1)$$. Since $$x^2 + 1$$ is irreducible in $$\mathbb{R}$$ (as $$\mathbb{\sqrt{-1}}$$ does not exist in $$\mathbb{R}$$) the resulting elements $$a + bi \in \mathbb{C}$$ contain a "real part" $$a$$ and an imaginary part $$b$$ with $$i = \sqrt{-1}$$. All field extensions are themselves fields.

We can do the same thing with finite fields. As an example, we can construct $$\mathbb{F}_{p^2} : \mathbb{F}[u] / (u^2 - \beta)$$ as a quadratic field extension over $$\mathbb{F}_p$$ so long as $$\beta$$ is quadratic nonresidue (nonsquare) in $$\mathbb{F}_p$$. We write its elements as $$c_0 + c_1 u$$.

In order to simplify arithmetic, we typically construct extension fields of large degree using "towers" of extension fields. As an example, we can construct the extension field $$\mathbb{F}_{p^{12}}$$ using a sequence of extensions:

* $$\mathbb{F}_{p^{2}}$$ is constructed as $$\mathbb{F}_{p}[u] / (u^2 - \beta)$$ for some quadratic nonresidue $$\beta \in \mathbb{F}_p$$.
* $$\mathbb{F}_{p^{6}}$$ is constructed as $$\mathbb{F}_{p^{2}}[v] / (v^3 - \gamma)$$ for some cubic nonresidue $$\gamma \in \mathbb{F}_{p^{2}}$$.
* $$\mathbb{F}_{p^{12}}$$ is constructed as $$\mathbb{F}_{p^{6}}[w] / (w^2 - \delta)$$ for some quadratic nonresidue $$\delta \in \mathbb{F}_{p^{6}}$$.

The precise choice of $$\beta, \gamma, \delta$$ doesn't affect arithmetic but may impact performance, and so certain classes of $$p$$ are typically sought so that efficient choices of these parameters can be made.
