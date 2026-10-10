# The First Theorem of Graph Theory

A well-known theorem in graph theory dealing with the sum of the degrees of the vertices of a graph was observed (indirectly) by Leonhard Euler in a 1736 paper [86] of his that is now considered the first paper ever written on graph theory – even though graph theorists were never mentioned in the paper. This observation is often referred to as the **First Theorem of Graph Theory**. Some have called Theorem 1.4 the **Handshaking Lemma**, although Euler never used this name.

# **Theorem 1.4 (The First Theorem of Graph Theory)**

If *G* is a graph of size *m*, then

```
∑_{v∈V(G)} deg v = 2m.
```

**Proof.** When summing the degrees of the vertices of *G*, each edge of *G* is counted twice, once for each of its two incident vertices.

The sum of the degrees of the vertices of the graph *G* of Figure 1.4 is 12, which is twice the size 6 of *G*, as expected from Theorem 1.4. The **average degree** of a graph *G* of order *n* and size *m* is

```
∑_{v∈V(G)} deg v / n = 2m/n.
```

For example, the average degree of the graph *G* of Figure 1.4 (having order *n* = 5 and size *m* = 6) is 2*m*/n = 12/5. Since the average degree of this graph is strictly between 2 and 3, it follows that *G* must have a vertex of degree 3 or more and a vertex of degree 2 or less. This graph actually has vertices of degrees 3 and 4 as well as vertices of degrees 1 and 2.

# Even and Odd Vertices

A vertex in a graph *G* is **even** or **odd**, according to whether its degree in *G* is even or odd. Thus, the graph *G* of Figure 1.4 has three even vertices and two odd vertices. While a graph can have either an even or an odd number of even vertices, this is not the case for odd vertices.

# **Corollary 1.5**

*Every graph has an even number of odd vertices.*

**Proof.** Suppose that *G* is a graph of size *m*. By Theorem 1.4,

```
∑_{v∈V(G)} deg v = 2m,
```

which, of course, is an even number. Since the sum of the degrees of the even vertices of *G* is even, the sum of the degrees of the odd vertices of *G* must be even as well, implying that *G* has an even number of odd vertices.