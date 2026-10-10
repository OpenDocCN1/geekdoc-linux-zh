As $n$ tends to infinity, the first factor in the expression for $E[X]$ tends to $\infty$ (as a polynomial in $n$) and the second factor tends to 0 exponentially. As we saw earlier in (21.2), this implies that $\lim _ { n \to \infty } E [ X ] = 0 .$

The basic idea used to define the random variable $X$ in the proof of Theorem 21.6 was generalized by Andreas Blaß and Frank Harary [29] in order to study other properties of almost all graphs.

For fixed nonnegative integers $k$ and $\ell$, let $Q _ { k , \ell }$ denote the property that if $S$ and $T$ are disjoint sets of vertices of a graph with $|S| \leq k$ and $|T| \leq \ell$, then there is a vertex $z \notin S \cup T$ that is adjacent to every vertex of $S$ and to no vertex of $T$. As is normally done, the statement of Theorem 21.7 below does not include the phrase “in $G ( n , p )$”. Since we are referring to “almost all graphs”, this is implied from the definition.

# Theorem 21.7 For each pair $k, \ell$ of nonnegative integers and each positive constant $p<1$, almost all graphs have property $Q _ { k , \ell }$.

# Proof.

Define a pair $\{ S , T \}$ of disjoint subsets of vertices of a graph with $|S| \leq k$ and $|T| \leq \ell$ to be bad if no vertex $z \notin S \cup T$ is adjacent to every vertex of $S$ and to no vertex of $T$. For each graph $G$ in $G ( n , p )$, let $X ( G )$ be the number of bad pairs $\{ S , T \}$ in $G$. We wish to show that almost all graphs have no bad pairs of sets and, as in the proof of Theorem 21.6, we need only show that $\lim _ { n \to \infty } E [ X ] = 0 .$

For each graph $G$ in $G ( n , p )$, list all pairs $\{ S , T \}$ of disjoint subsets of vertices of $G$. The variable $X ( G )$ can be written as the sum of indicator variables $X _ { i }$, where $X _ { i } = 1$ if the $i$th pair $\{ S , T \}$ is bad and $X _ { i } = 0$ otherwise. For a fixed pair $\{ S , T \}$ and a vertex $z \notin S \cup T$, the probability that $z$ is adjacent to every vertex of $S$ and to no vertex of $T$ is $p ^ { | S | } ( 1 - p ) ^ { | T | }$. Since

```
$$p ^ { | S | } ( 1 - p ) ^ { | T | } \, \geq p ^ { k } ( 1 - p ) ^ { \ell } ,$$
```

the probability that the pair $S , T$ is bad, that is, that no such $z$ exists for the pair $\{ S , T \}$, is

```
$$\left( 1 - p ^ { | S | } ( 1 - p ) ^ { | T | } \right) ^ { n - | S | - | T | } \, \leq \, \left( 1 - p ^ { k } ( 1 - p ) ^ { \ell } \right) ^ { n - k - \ell } .$$
```

In other words,

```
$$P [ X _ { i } = 1 ] \leq \left( 1 - p ^ { k } ( 1 - p ) ^ { \ell } \right) ^ { n - k - \ell } .$$
```