Applying Theorem 14.25 to both a graph $G$ of order $n$ and its complement $\overline{G}$ (where then $\omega(G)=\alpha(G)$ and $\alpha(\overline{G})=\omega(G)$), we have

```
$$\chi(G) \leq \frac{\omega(G)+n+1-\alpha(G)}{2}$$
```

and

```
$$\chi(\overline{G}) \leq \frac{\omega(\overline{G})+n+1-\alpha(\overline{G})}{2}.$$
```

Adding these inequalities gives us an alternative proof of the major inequality stated in the Nordhaus-Gaddum theorem (Theorem 14.23): For every graph $G$ of order $n$,

```
$$\chi(G)+\chi(\overline{G}) \leq n+1.$$
```

# The Gallai-Roy-Vitaver Theorem

Bounds for the chromatic number of a graph $G$ can also be given in terms of the length $\ell(D)$ of a longest (directed) path in an orientation $D$ of $G$. Suppose that $G$ is a $k$-chromatic graph, where a $k$-coloring of $G$ is given using the colors 1, 2, …, $k$. An orientation $D$ of $G$ can be constructed by directing each edge $uv$ of $G$ from $u$ to $v$ if the color assigned to $u$ is smaller than the color assigned to $v$. Thus, the length of every directed path in $D$ is at most $k-1$. In particular, $\ell(D) \leq \chi(G)-1$. So, there exists an orientation $D$ of $G$ such that $\chi(G) \geq 1+\ell(D)$. On the other hand, Tibor Gallai [100], Bernard Roy [212] and L. M. Vitaver [245] independently discovered the following result.

**Theorem 14.26 (The Gallai-Roy-Vitaver Theorem)** *For every orientation $D$ of a graph $G$,*

```
$$\chi(G) \leq 1+\ell(D).$$
```

**Proof.** Let $D$ be an orientation of $G$ and let $D'$ be a spanning acyclic subdi-graph of $D$ of maximum size. A coloring $c$ is defined on $G$ by assigning to each vertex $v$ of $G$ the color 1 plus the length of a longest path in $D'$ whose terminal vertex is $v$. Then, as we proceed along the vertices in any directed path in $D'$, the colors are strictly increasing.

Let $(u, v)$ be an arc of $D$. If $(u, v)$ belongs to $D'$, then $c(u)<c(v)$. On the other hand, if $(u, v)$ is not in $D'$, then adding $(u, v)$ to $D'$ creates a directed cycle, which implies that $c(v)<c(u)$. Consequently, $c(u) \neq c(v)$ for every two adjacent vertices $u$ and $v$ of $G$ and so

```
$$c:V(G) \rightarrow \{1, 2, \ldots, 1+\ell(D)\}$$
```

is a proper coloring of $G$. Therefore, $\chi(G) \leq 1+\ell(D)$. ■

The following result is therefore a consequence of Theorem 14.26 and the observation that precedes it.