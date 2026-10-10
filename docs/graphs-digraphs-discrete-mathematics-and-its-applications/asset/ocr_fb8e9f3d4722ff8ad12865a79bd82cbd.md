# **Theorem 16.16** $\chi(S_t) = 7.$

**Proof.** In Figure 11.17, we saw that the complete graph $K_7$ can be embedded on the torus. Since $\chi(K_7) = 7$, it follows that $\chi(S_1) \geq 7.$

Now, let $G$ be a graph that can be embedded on the torus. Among the subgraphs of $G$, let $H$ be one having the largest minimum degree. We show that $\delta(H) \leq 6.$ Suppose that $H$ has order $n$ and size $m.$ If $n \leq 7$, then certainly $\delta(H) \leq 6.$ Hence, we may assume that $n > 7.$

Since $G$ is embeddable on the torus, so is $H.$ Thus, $\gamma(H) \leq 1.$ It therefore follows by Theorem 11.13 that

$$1 \geq \gamma(H) \geq \frac{m}{6} - \frac{n}{2} + 1$$
and so $m \leq 3n.$ Hence,

$n \delta(H) \leq \sum_{v \in V(H)} \deg_H v = 2m \leq 6n$
and so $\delta(H) \leq 6.$ Therefore, in any case, $\delta(H) \leq 6.$ By Theorem 14.19, $\chi(G) \leq 1 + \delta(H) \leq 7.$

Thus, $\chi(S_1) = 7.$

In his important paper, Heawood [125] obtained an upper bound for the chromatic number of $S_k$ for every positive integer $k.$

# **Theorem 16.17** For every nonnegative integer $k,$

$$\chi(S_k) \leq \left[ \frac{7 + \sqrt{1 + 48k}}{2} \right].$$

**Proof.** Let $G$ be a graph that is embeddable on the surface $S_k$ and let