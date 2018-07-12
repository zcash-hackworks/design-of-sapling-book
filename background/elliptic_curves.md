# Elliptic Curves

Consider an (appropriately designed) [elliptic curve](https://en.wikipedia.org/wiki/Elliptic-curve_cryptography) $$E$$ over some field $$\mathbb{F}$$:

$$
E(\mathbb{F}) : y^2 = x^3 + b
$$

All of the solutions $$(x, y)$$ to this equation are called the **affine** points of $$E$$. The points on this curve happen to form a group $$\mathbb{G}$$ with an additive identity $$\infty$$ called the "point at infinity."

* The additive inverse of an affine point $$(x, y)$$ is the point $$(x, -y)$$, and the additive inverse of $$\infty$$ is $$\infty$$.
* If two affine points are additive inverses, their sum is $$\infty$$. Otherwise, their sum is found by finding the line intersecting the two points (or the tangent line if the two points are the same) and finding the third point on the curve that intersects it, and then negating its y-coordinate.


# TODO

Explain more about elliptic curves.

1. Different kinds of elliptic curves
2. Discrete log problem
3. Computational/Decisional Diffie-Hellman problems
4. Knowledge of exponent assumption?
