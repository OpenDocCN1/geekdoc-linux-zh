and so $\chi'(G) = k \geq \frac{m}{\alpha'(G)}$.\hspace{4mm}

Since every edge coloring of a graph $G$ must assign distinct colors to adjacent edges, it follows for each vertex $v$ of $G$ that deg $v$ colors must be used to color the edges incident with $v$. Therefore,

> $$\chi'(G) \geq \Delta(G)\tag{17.1}$$

for every nonempty graph $G$.

In the graph $G$ of order $n = 7$ and size $m = 10$ of Figure 17.2, $\Delta(G) = 3$. Hence, $\chi'(G) \geq 3$ by (17.1). Furthermore, since $X = \{uz, vx, wy\}$ is an independent set of three edges of $G$ and $\alpha'(G) \leq n/2 = 7/2$, it follows that $\alpha'(G) = 3$. However, by Theorem 17.1, $\chi'(G) \leq m/\alpha'(G) = 10/3$ and so we arrive at an even larger lower bound for $\chi'(G)$, namely $\chi'(G) \geq 4$. The 4-edge coloring of $G$ in Figure 17.2 shows that $\chi'(G) \leq 4$ and so $\chi'(G) = 4$.

![](bbox=[0.1, 0.44, 0.9, 0.63])

# **Vizing's Theorem**

While $\Delta(G)$ is a rather obvious lower bound for the chromatic index of a nonempty graph $G$, the graph $G$ of Figure 17.2 shows that it's possible that $\chi'(G) > \Delta(G)$. The Russian graph theorist Vadim G. Vizing [246] established a remarkable upper bound for the chromatic index of a graph. Vizing's theorem, published in 1964, must be considered the major theorem in the area of edge colorings. Vizing's theorem was rediscovered in 1966 by Ram Prakash Gupta [110].

# **Theorem 17.2 (Vizing's Theorem)** $For$ $every$ $nonempty$ $graph$ $G$,

> $$\chi'(G) \leq 1 + \Delta(G).$$

**Proof.** Suppose that the theorem is false. Then among all those graphs $H$ for which $\chi'(H) \geq 2 + \Delta(H)$, let $G$ be one of minimum size and let $\Delta = \Delta(G)$,