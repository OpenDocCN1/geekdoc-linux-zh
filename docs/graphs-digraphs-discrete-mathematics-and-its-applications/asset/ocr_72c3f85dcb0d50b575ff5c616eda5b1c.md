backward arcs $a_i$. If only one of $p_1$ and $p_2$ is defined, then denote this number by $p$; otherwise, let $p = \min\{p_1, p_2\}$.

Define a function $f'$ on $E(D)$ by

$f'(a) = \begin{cases} f(a) + p & \text{if } a \text{ is a forward arc on } P \\ f(a) - p & \text{if } a \text{ is a backward arc on } P \\ f(a) & \text{if } a \notin E(P). \end{cases}$

Then $f'$ is also a flow. Since $\text{val}(f') = \text{val}(f) + p$, it follows that $f$ is not a maximum flow.

We now turn to the converse. Assume that there is no $f$-augmenting semipath in $D$. Let $X$ be the set of all vertices $x$ in $D$ for which there exists an $f$-unsaturated $u-x$ semipath. Then $u \in X$ and, by assumption, $v \notin X$. Thus, $K = [X, \bar{X}]$ is a cut in $N$.

Let $(y, z)$ be an arc in $K$. Since $y \in X$, there exists an $f$-unsaturated $u-y$ semipath $P$ in $D$. Since $z \in \bar{X}$, there is no $f$-unsaturated $u-z$ semipath in $D$, which implies that $f(y, z) = c(y, z)$. Similarly, if $(w, x) \in [\bar{X}, X]$, then $f(w, x) = 0$. Since $K = [X, \bar{X}]$ is a cut such that $f(a) = c(a)$ for every arc $a \in [X, \bar{X}]$ and $f(a) = 0$ for every arc $a \in [\bar{X}, X]$, it follows by Corollary 8.4 that $f$ is a maximum flow.

# 8.2 The Max-Flow Min-Cut Theorem

With the aid of Theorem 8.5, Ford and Fulkerson [93] proved a famous result in 1956 that is known as the Max-Flow Min-Cut Theorem. Independently, and also in 1956, Peter Elias, Amiel Feinstein and Claude Elwood Shannon [77] discovered and proved the very same result.

Theorem 8.6 (The Max-Flow Min-Cut Theorem) In any network, the value of a maximum flow equals the capacity of a minimum cut.

**Proof.** Let $f$ be a maximum flow in a network $N$ having capacity function $c$. By Theorem 8.5, there is no $f$-augmenting semipath in the underlying digraph $D$ of $N$. By the proof of Theorem 8.5, since $D$ contains no $f$-augmenting semipath, there is a minimum cut $K = [X, \bar{X}]$ such that

$f(a) = \begin{cases} c(a) & \text{if } a \in K \\ 0 & \text{if } a \in [\bar{X}, X]. \end{cases}$

Therefore, by (8.8),

$\begin{aligned} \text{val}(f) & = f^+(X) - f^-(X) = f(X, \bar{X}) - f(\bar{X}, X) \\ & = c(X, \bar{X}) - 0 = \text{cap}(K), \end{aligned}$

as desired.