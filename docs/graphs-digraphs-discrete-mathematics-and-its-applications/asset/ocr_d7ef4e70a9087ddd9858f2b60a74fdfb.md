**Proof.** First, suppose that $g$ is odd. Then $g = 2k+1$ for some positive integer $k$. Let $v \in V(G)$. For $1 \le i \le k$, the number of vertices at distance $i$ from $v$ is $r(r-1)^{i-1}$. Since the girth of $G$ is $g = 2k+1$, no two vertices of $G$ at distance $i$ from $v$ can be adjacent to a vertex of distance $i$ or $i-1$ from $v$ if $i \le (g-5)/2$. From this, it follows that

```
```
n \quad \ge \quad 1+r+r(r-1)+r(r-1)^2+\cdots+r(r-1)^{k-1}
\quad = \quad 1+r+r(r-1)+r(r-1)^2+\cdots+r(r-1)^{(g-3)/2}.
```
```

Next, suppose that $g$ is even. Then $g = 2k$ where $k \ge 2$. Let $e = uv \in E(G)$. For $1 \le i \le k-1$, the number of vertices at distance $i$ from $u$ or $v$ is $2(r-1)^i$. Here,

```
```
n \quad \ge \quad 2+2(r-1)+2(r-1)^2+\cdots+2(r-1)^{k-1}
\quad \ge \quad 2\Big[ 1+(r-1)+(r-1)^2+\cdots+(r-1)^{(g-2)/2} \Big].
```
```

Thus, $n \ge M(r,g)$.

For integers $r \ge 2$ and $g \ge 3$, the smallest order of an $(r,g)$-graph is denoted by $n(r,g)$. The $r$-regular graphs of order $n(r,g)$ having girth $g$ are called $(r,g)$-cages. Thus, among the $(r,g)$-graphs, an $(r,g)$-cage is one of minimum order. The $(3,g)$-cages are the most studied of these graphs and are commonly referred to simply as $g$-cages. Therefore, a $g$-cage is a cubic graph of minimum order having girth $g$.

# **Existence of Cages**

The most fundamental question now is the following: For which pairs $r,g$ of integers with $r \ge 2$ and $g \ge 3$, does there exist an $(r,g)$-graph? Of course, if there exists even one $(r,g)$-graph, then there is an $(r,g)$-cage, perhaps more than one. If there exists an $(r,g)$-graph for given integers $r \ge 2$ and $g \ge 3$, then $n(r,g) \ge \max\{r+1,g\}$. Since $C_9$ is a 2-regular graph of girth 9, it follows that $n(2,g)$ exists and $n(2,g) = g$. Likewise, $n(r,3) = r+1$ since $K_{r+1}$ is an $r$-regular graph having girth 3. In fact, the complete graph $K_4$ is the unique 3-cage. The following result of Paul Erdős and Homet Sachs [83] not only establishes the existence of a cage for each pair $r,g$ but provides an upper bound on their orders.

**Theorem 19.9** For every pair $r,g$ of integers with $r \ge 2$ and $g \ge 3$, the number $n(r,g)$ exists and

```
```n(r,g) \le 3(r-1)+2\big[ (r-1)^2+(r-1)^3+\cdots+(r-1)^{[g/2]}\big]+(r-1)^{g-1}.
```
```

**Proof.** Since $n(2,g) = g$ for $g \ge 3$ and $n(r,3) = r+1$ for $r \ge 2$, we may assume that $r \ge 3$ and $g \ge 4$. Let