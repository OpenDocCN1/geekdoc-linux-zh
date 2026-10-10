![](bbox=[0.25, 0.08, 0.75, 0.28])

Figure 8.3: The cut $[X, \bar{X}]$ in the network $N$ of Figure 8.2 for $X = \{u, x\}$

If $K$ is a cut in a network $N$, then any path from the source $u$ to the sink $v$ must contain at least one arc of $K$. Consequently, if all arcs of $K$ were removed from the underlying digraph $D$ of $N$, then there would be no path from $u$ to $v$. So just as a vertex-cut in a graph $G$ separates some pair of vertices in $G$ and an edge-cut in $G$ separates some pair of vertices in $G$, a cut in the underlying digraph $D$ of a network $N$ separates $u$ and $v$ in a certain sense.

Let $N$ be a network with underlying digraph $D$, source $u$ and sink $v$. For a set $X$ of vertices of $D$ with $u \in X$ and $v \in \bar{X}$ and a flow $f$ defined on $N$, the **net flow out** of $X$ is $f^{+}(X) - f^{-}(X)$ and the **net flow into** $X$ is $f^{-}(X) - f^{+}(X)$. It then follows (see Exercise 8) that

```
$$ f^{+}(X) - f^{-}(X) = f(X, \bar{X}) - f(\bar{X}, X). \tag{8.8} $$
```

For the set $X = \{u, x, t\}$ in the network $N$ in Figure 8.2, $f^{+}(X) = 10$ and $f^{-}(X) = 7$. For this network then, the net flow out of $X$ is $f^{+}(X) - f^{-}(X) = 10 - 7 = 3 = \text{val}(f)$. We now show that for a network $N$ and any cut $K = [X, \bar{X}]$ in $N$, the value of any flow in $N$ is the net flow out of $X$ and that this value never exceeds the capacity of $K$.

**Theorem 8.2** *Let $f$ be a flow in a network $N$ and let $K = [X, \bar{X}]$ be a cut in $N$. Then*

```
$$ \text{val}(f) = f^{+}(X) - f^{-}(X) \leq \text{cap}(K). $$
```

**Proof.** Let $D$ be the underlying digraph of $N$, let $u$ and $v$ be the source and sink, respectively, of $N$ and let $c$ be the capacity function of $N$.

Since $f^{+}(x) - f^{-}(x) = 0$ for every $x \in X - \{u\}$, it follows that

```
$$ \sum_{x \in X} (f^{+}(x) - f^{-}(x)) = f^{+}(u) - f^{-}(u) = \text{val}(f). $$
```

Furthermore,

```
$$ \sum_{x \in X} (f^{+}(x) - f^{-}(x)) = \sum_{x \in X} f^{+}(x) - \sum_{x \in X} f^{-}(x) = f^{+}(X) - f^{-}(X) $$
```