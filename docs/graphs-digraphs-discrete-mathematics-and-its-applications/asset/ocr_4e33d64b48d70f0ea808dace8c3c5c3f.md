# 6.5. POWERS OF GRAPHS AND LINE GRAPHS



The vertex $v_{j_{2}-1}$ is incident with $e_{j_{2}}$, the vertex $v_{j_{2}}$ is incident with $e_{j_{2}}$ and $v_{j_{2}-1} = v_{j_{1}}$. Thus, $e_{j_{2}} = v_{j_{1}}v_{j_{2}}$. Continuing in this fashion, we finally arrive at a vertex $v_{j_{k}}$ such that $e_{j_{k}} = v_{j_{k}-1}v_{j_{k}}$, where $v_{j_{k}} = v_{m-1}$. Since every edge of $G$ appears exactly once in $s$ and since $1 < j_{1} < j_{2} < \cdots < j_{k} = m-1$, this construction yields a trail

```
$T = (v_{1}, e_{j_{1}}, v_{j_{1}}, e_{j_{2}}, v_{j_{2}}, \cdots, v_{j_{k-1}}, e_{j_{k}}, v_{j_{k}} = v_{m-1})$
```

in $G$ with the properties that (i) every edge of $G$ is incident with a vertex of $T$ and (ii) neither $e_{1}$ nor $e_{m}$ is an edge of $T$.
Let $w$ be the vertex of $G$ incident with both $e_{1}$ and $e_{m}$. We consider four possible cases.

+   - Case 1. $w = v_{1} = v_{m-1}$. Then $T$ itself is a dominating circuit of $G$.
+   - Case 2. $w = v_{1}$ and $w \neq v_{m-1}$. Since $e_{m}$ is incident with both $w$ and $v_{m-1}$, it follows that $e_{m} = v_{m-1}w = v_{m-1}v_{1}$. Thus, $C = (T, e_{m}, v_{1})$ is a dominating circuit of $G$.
+   - Case 3. $w = v_{m-1}$ and $w \neq v_{1}$. Since $e_{1}$ is incident with both $w$ and $v_{1}$, we have that $e_{1} = wv_{1} = v_{m-1}v_{1}$. Thus, $C = (T, e_{1}, v_{1})$ is a dominating circuit of $G$.
+   - Case 4. $w \neq v_{m-1}$ and $w \neq v_{1}$. Since $e_{m}$ is incident with both $w$ and $v_{m-1}$, it follows that $e_{m} = v_{m-1}w$. Because $e_{1}$ is incident with both $w$ and $v_{1}$, we have that $e_{1} = wv_{1}$. Thus, $v_{1} \neq v_{m-1}$ and $C = (T, e_{m}, w, e_{1}, v_{1})$ is a dominating circuit of $G.$

As a consequence of Theorem 6.27, if $G$ is either Eulerian or Hamiltonian, then $L(G)$ is Hamiltonian. In fact, successively taking the line graph of a connected graph has some interesting consequences.
For a nonempty graph $G$, we write $L^{k}(G)$ to denote $G$ and $L^{k}(G)$ to denote $L(G)$. For an integer $k \geq 2$, the iterated line graph $L^{k}(G)$ is defined as $L(L^{k-1}(G))$, where $L^{k-1}(G)$ is assumed to be nonempty. The following result is due to Gary Lohr and Curtiss E. Wall [51].

# **Theorem 6.28** If $G$ is a connected graph such that $\deg v \geq 3$ for every vertex $v$ of $G$, then $L^{2}(G)$ is Hamiltonian.

**Proof.** Let $v$ be a vertex of $G$, where $\deg v = r \geq 3$. Then in $L(G)$, the edges incident with $v$ give rise to a subgraph $H_{v}$, where $H_{v} \cong K_{r}$. Let $C_{v}$ be a Hamiltonian cycle in $H_{v}$. Let $H$ be the spanning subgraph of $L(G)$ defined by

$V(H) = V(L(G))$ and $E(H) = \cup_{v \in V(G)} E(C_{v}).$

Then $H$ is connected and every vertex of $H$ is even. Consequently, $H$ is Eulerian and so $H$ is a dominating circuit of $L(G)$. By Theorem 6.27, $L^{2}(G)$ is Hamiltonian.