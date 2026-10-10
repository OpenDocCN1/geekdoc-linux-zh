this after generalizing (wrongly) from “three vertices give a triangle” to “four vertices give an (ordinary) quadrilateral.” Rather K₄ is what is called a “complete quadrilateral”: a quadrilateral together with its diagonals.

It is rather a mouthful to have to keep talking about, for example, “a subgraph isomorphic to K₃, all of whose edges are red.” So we introduce some terminology that enables us to abbreviate our statements.

# DEFINITION 16.2

Suppose that the edges of the graph Kₙ are colored using red and blue and p is a positive integer. We say that Kₙ has a red Kₚ if there is a set, say P, of p vertices of Kₙ, such that all the edges joining pairs of vertices of P are red (that is, Kₙ has a subgraph isomorphic to Kₚ, all of whose edges are red). We say that Kₙ has a blue Kₚ if we can find a set P of p vertices such that all the edges joining them are blue.

In terms of this definition we can rephrase the result of Problem 16A by saying that if the edges of K₆ are colored using red or blue, then K₆ has either a red K₄ or a blue K₃.

We now introduce the following definition, which is the special case of the definition of F(s : t₁, t₂, …, tₖ) with s = k = 2, t₁ = p, and t₂ = q.

# DEFINITION 16.3

Let p, q be positive integers with p, q ≥ 2 such that there exists an integer n with the property that, however the edges of the complete graph, Kₙ, are colored red and blue, Kₙ will always have either a red Kₚ or a blue K_q. Then there will be a smallest integer, n, with this property. This smallest integer n is called the (p, q) Ramsey number and written as R(p,q).

For example, our discussion above shows that R(3, 3) = 6. Because of the symmetry between red and blue in Definition 16.3 the following result is obvious.

# THEOREM 16.1

For all positive integers p, q, if R(p, q) exists, then so also does R(q, p), and we have that R(p, q) = R(q, p).

We now face an infinity of questions! Does R(p, q) exist for each pair of integers p, q? If so, what is its value? For example, what (if they exist) are R(3, 4) and R(4, 4)?

Of course, Ramsey’s theorem implies that R(p, q) always exists, but we have not yet given a proof of this. We give a proof in the case p, q ≥ 3 in Theorem 16.3, but first we determine the exact value of R(2, q) for all q ≥ 2.

# THEOREM 16.2

For all p, q ≥ 2, R(p, 2) = p and R(2, q) = q.

# Proof

This is straightforward, since if each edge of the complete graph Kₙ is either red or blue, then either every edge is red, in which case we have p vertices joined by edges that are all red, or there is a blue edge, say {u, v}, in which case we have a set of two