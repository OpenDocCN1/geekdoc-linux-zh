Since $\pi$ is a permutation of $D$, the set of values taken by $\pi \circ (d)$ as $d$ runs through $D$ is just $D$ itself. Hence the product in the right-hand term of Equation 14.16 is the same as $\prod_{d \in D} w(f(d)) = W(f)$. Thus it follows that $W(g) = W(f)$.

We have now seen that for each set $X_i$ of the partition of $X$ determined by the weight of the functions, if $f \in X_x$, then $\pi \circ f \in X_x$. In this sense $G$ acts separately on each set $X_x$. We use the notation $\pi_x$ to indicate that we are restricting our attention to the action of the permutation $\pi$ on the set $X_x$. We can then apply Frobenius's counting theorem to count the number of orbits of the action of $G$ on each set $X_x$. This enables us to prove P\'olya's counting theorem, which, for convenience, we restate.

# **THEOREM 14.3**

**P\'olya's Counting Theorem**

Let $X$ be the set of all mappings from a set $D$ to a set $C$, and let $w$ be a weight function on $C$. Let $G$ be a group of permutations of $D$ whose action on $X$ is given by:

> $\forall \pi \in G, \text{ and } f \in X, \quad \pi \circ f = f \circ \pi^{-1}.$

Then the pattern inventory is obtained from the cycle index of $G$, by substituting $\sum_{c \in C} w(c)^k$ for $x_k$, for $k = 1,2,3,\ldots$. Thus if $CI(G)(x_1,x_2,x_3,\ldots)$ is the cycle index of $G$, the pattern inventory is

> $$CI(G)\bigg( \sum_{c \in C} w(c), \sum_{c \in C} w(c)^2, \sum_{c \in C} w(c)^3, \ldots \bigg) . \qquad (14.8)$$

# **Proof**

We let $PI$ be the pattern inventory. Suppose that $W_i$ is the common weight of all the functions in the set $X_i$ of the partition, and that there are $m_i$ different patterns represented by the functions in $X_i$. We have seen, from Lemma 14.7, that no pattern is represented by functions in more than one of the sets of the partition. It follows that

> $$PI = \sum_{i=1}^i m_i W_i. \qquad$$

By Frobenius's counting theorem,

> $$m_i = \frac{1}{\#(G)} \sum_{\pi \in G} \#(\text{Fix}(\pi_i)), \qquad$$

and hence

> $$PI = \frac{1}{\#(G)} \bigg( \sum_{i=1}^i \sum_{\pi \in G} \#(\text{Fix}(\pi_i)) \, W_i \bigg). \qquad (14.17)$$