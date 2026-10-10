**Proof.** Let $D$ be an orientation of $G$ having a nowhere-zero $k$-flow $\phi$. Thus, $\sigma^{+}(v; \phi) = \sigma^{-}(v; \phi)$ for each vertex $v$ of $D$. Let $D'$ be the orientation of $G$ obtained by reversing the direction of some arc $f=(x,y)$ of $D$, resulting in the arc $f'=(y,x)$ of $D'$. We now define the function

```
$\phi' : E(D') \rightarrow \{\pm 1, \pm 2, \ldots, \pm (k-1)\}$
```

by

```
$$\phi'(e) \quad = \quad \left\{ \begin{array}{l l} \phi(e) & \text{if } e \neq f' \\ -\phi(f) & \text{if } e = f'. \end{array} \right.$$
```

For $v \in V(D) - \{x,y\}$, $\sigma^{+}(v; \phi') = \sigma^{-}(v; \phi')$. Also,

```
$\begin{array}{rcl} \sigma^{+}(x; \phi') & = & \sigma^{+}(x; \phi) - \phi(f) = \sigma^{-}(x; \phi) + \phi'(f') = \sigma^{-}(x; \phi') \\ \sigma^{+}(y; \phi') & = & \sigma^{+}(y; \phi) + \phi'(f') = \sigma^{-}(y; \phi) + (-\phi(f)) = \sigma^{-}(y; \phi'). \end{array}$
```

Thus, $\phi'$ is a nowhere-zero $k$-flow of $D'$.

Now, if $D''$ is any orientation of $G$, then $D''$ can be obtained from $D$ by a sequence of arc reversals in $D$. Since a nowhere-zero $k$-flow can be defined on each orientation, as described above, at each step of the sequence, a nowhere-zero $k$-flow can be defined on $D''$.

According to Theorem 18.2, the property of an orientation (indeed of *all orientations*) of a graph $G$ having a nowhere-zero $k$-flow is a characteristic of $G$ rather than a characteristic of its orientations. We therefore say that a **graph** $G$ has a **nowhere-zero $k$-flow** if every orientation of $G$ has a nowhere-zero $k$-flow. As a consequence of the proof of Theorem 18.2, we also have the following.

# **Theorem 18.3** If $G$ is a graph having a nowhere-zero $k$-flow for some $k \geq 2$, then there is an orientation $D$ of $G$ and a nowhere-zero $k$-flow on $D$ all of whose flow values are positive.

By Theorem 18.1, the graph $G$ of Figure 18.2 does not have a nowhere-zero 2-flow. Trivially, it has an orientation $D$ possessing a 2-flow. This orientation does have a nowhere-zero 3-flow, however. By Theorem 18.2, $G$ itself has a nowhere-zero 3-flow.

![](bbox=[0.07, 0.86, 0.93, 0.95])

Figure 18.2: A graph with a nowhere-zero 3-flow