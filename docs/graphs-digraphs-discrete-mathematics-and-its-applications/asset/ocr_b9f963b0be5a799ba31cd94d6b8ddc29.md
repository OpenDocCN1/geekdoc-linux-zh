Corresponding to each 1-factor $F_i$ of $H$ is a permutation $\alpha_i$ on the set $\{1,2,\dots,n\}$, defined by $\alpha_i(j)=j$ if $u_jw_j\in E(F_i)$. Let $\alpha_i$ be expressed as a product of disjoint permutation cycles. There is no permutation cycle of length 1 in this product; for if $(i)$ were a permutation cycle, then this would imply that $\alpha_i(i)=i$. However, this further implies that $u_iv_i\in E(F_i)$ and that $v_iv_i\in E(C)$, which is impossible. Also, there is no permutation cycle of length 2 in this product; for if $(ij)$ were a permutation cycle, then $\alpha_i(j)=j$ and $\alpha_i(j)=i$. This would indicate that $u_iw_j,u_jw_i\in E(F_i)$ and that $v_j$ both immediately follows and precedes $v_i$ on $C$, contradicting the fact that no edge is repeated on a circuit. Thus, the length of every permutation cycle in $\alpha_i$ is at least 3.

Each permutation cycle in $\alpha_i$ therefore gives rise to a cycle in $G$, and the product of the disjoint permutation cycles in $\alpha_i$ produces a collection of mutually disjoint cycles in $G$ containing all vertices of $G$, that is, a 2-factor in $G$. Since the 1-factors in $H$ are mutually edge-disjoint, the resulting 2-factors in $G$ are mutually edge-disjoint. Hence, $G$ is 2-factorable.

To illustrate the proof of Theorem 13.4, let $G=K_{2,2,2}$ be the 4-regular graph of order 6 shown in Figure 13.4(a). An Eulerian circuit of $G$ is

```
$C=(v_1,v_2,v_3,v_1,v_2,v_5,v_6,v_3,v_5,v_4,v_1)$.
```

Following the proof of Theorem 13.4, we construct the bipartite graph $H$ shown in Figure 13.4(b) having partite sets $U=\{u_1,u_2,\dots,u_6\}$ and $W=\{w_1,w_2,\dots,w_6\}$. Since $v_1v_2\in E(C)$, it follows that $u_1w_2\in E(H)$. Similarly, $u_2w_3,u_3w_1\in E(H)$ and so on. Figure 13.4(c) shows one possible 1-factorization of $H$ into the two 1-factors $F_1$ and $F_2$. Corresponding to $F_1$ and $F_2$ are the permutations below:

```
$\alpha_1 \mathbin{=} \left( \begin{array} {cccccc} 1&2&3&4&5&6 \\ 2&3&1&6&4&5 \end{array} \right) \mathbin{=} (1\ 2\ 3)(4\ 6\ 5)$
$\alpha_2 \mathbin{=} \left( \begin{array} {cccccc} 1&2&3&4&5&6 \\ 5&6&4&1&2&3 \end{array} \right) \mathbin{=} (1\ 5\ 2\ 6\ 3\ 4)$.
```

These two permutations then give rise to the 2-factors $G_1$ and $G_2$ shown in Figure 13.4(d). Thus, $\{G_1,G_2\}$ is a 2-factorization of $G$.

# Hamiltonian Factorable Graphs

It is an immediate consequence of Theorem 13.4 that there exists a factorization of every regular graph $G$ of positive even degree in which every factor is a union of cycles. This brings up the problem of whether there exists a factorization of $G$ in which every factor is a single cycle, that is, a Hamiltonian cycle of $G$. A **Hamiltonian factorization** of a graph $G$ is a factorization of $G$ such that every factor is a Hamiltonian cycle of $G$ and a graph possessing such a factorization is **Hamiltonian factorable**. Certainly, every Hamiltonian