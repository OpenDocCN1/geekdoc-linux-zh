# LEMMA 14.6

If $ct(\pi) = x_{k_1}^{k_1} \cdots x_{k_r}^{k_r}$, then the inventory of $Fix(\pi)$ is

```
$$\left(\sum_{c \in C} w(c)^{k_1}\right) \times \left(\sum_{c \in C} w(c)^{k_2}\right) \times \ldots \times \left(\sum_{c \in C} w(c)^{k_r}\right) \tag{14.14}$$
```

or, equivalently,

```
$$ct(\pi)\left\{\sum_{c \in C} w(c), \sum_{c \in C} w(c)^2, \sum_{c \in C} w(c)^3, \ldots\right\}. \tag{14.15}$$
```

# Proof

The cycles of $\pi$ partition $D$ into $r_1$ sets of size $k_1$, $r_2$ sets of size $k_2$, and so on. By Lemma 14.4, $Fix(\pi)$ is the set of functions that are constant on all these sets, and hence, by Lemma 14.5, the inventory of $Fix(\pi)$ is as given by the formula 14.14. This formula is obtained from the cycle type of $\pi$ by replacing each occurrence of $x_k$ for $k=1,2,3, \ldots$ by $\sum_{c \in C} w(c)^k$. Hence we can rewrite this formula as given in the formula 14.15. This completes the proof.

We now partition $X$ into sets of functions with the same weight. Clearly, the relation $\sim$ defined on $X$ by

```
$f \sim g \Leftrightarrow W(f) = W(g)$
```

is an equivalence relation. We let $x_1, x_2, \ldots, X$, be the equivalence classes of this relation. So they form a partition of $X$. (For example, in our example of the colorings of a $2 \times 2$ chessboard, the set $X$ of all 16 colorings is partitioned according to the numbers of black and white squares in a particular coloring. So one of the equivalence classes is the set of all colorings with two black squares and two white squares, namely, $\{C6, C7, C8, C9, C10, C11\}$. Note that within this equivalence class there are two different patterns. You will also note that all the colorings of any one particular pattern lie in the same equivalence class. Our next result generalizes this observation.)

The next lemma implies that $G$ acts on each set of this partition separately.

# LEMMA 14.7

Suppose that $f,g \in X$ have the same pattern; that is, they occur in the same orbit of the group action. Then $W(f) = W(g)$.

# Proof

Suppose $f$ and $g$ are in the same orbit of the group action. Then for some $\pi \in G$, $\pi \circ f = g$, and thus $f \circ \pi^{-1} = g$, and hence

```
$$W(g) = \prod_{d \in D} w(g(d)) = \prod_{d \in D} w(f(\pi^{-1}(d))) \tag{14.16}$$
```