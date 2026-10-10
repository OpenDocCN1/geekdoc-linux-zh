In 1979 Jeffrey Howard Dinitz had already conjectured that $\chi_l^\prime(G)=\chi_l^\prime(G)$ when $G$ is a regular complete bipartite graph. By Theorem 17.7, it is known that $\chi^\prime(K_{r,r})=r$.

> **Dinitz’s Conjecture** For every positive integer $r$, $\chi_l^\prime(K_{r,r})=r$.

# Galvin’s Theorem

Fred Galvin [101] not only verified Dinitz’s Conjecture, he showed that the List Coloring Conjecture is true for all bipartite graphs (indeed, for all bipartite multigraphs). The proof of this result that we present is based on a proof of Tomáš Slivník [222], which in turn is based on Galvin’s proof. We begin with a lemma of Slivník. First, we introduce some notation. Let $G$ be a nonempty bipartite graph with partite sets $U$ and $W$. For each edge $e$ of $G$, let $u_e$ denote the vertex of $U$ incident with $e$ and let $w_e$ denote the vertex of $W$ incident with $e$. For adjacent edges $e$ and $f$, it therefore follows that $u_e=u_f$ or $w_e=w_f$, but not both.

# Lemma 18.16

Let $G$ be a nonempty bipartite graph and let $c:E(G)\to\mathbb{N}$ be an edge coloring of $G$. For each edge $e$ of $G$, let $\sigma_G(e)$ be the sum

```
$\begin{eqnarray*}\sigma_G(e)&=&1+|\{f\in E(G):u_e=u_f\text{ and }c(f)>c(e)\}|\\&+&|\{f\in E(G):w_e=w_f\text{ and }c(f)<c(e)\}|\end{eqnarray*}$
```

and let $\mathfrak{L}(e)$ be a set of $\sigma_G(e)$ colors. If

```
$$\mathfrak{L}=\{\mathfrak{L}(e):e\in E(G)\},$$
```

then $G$ is $\mathfrak{L}$-edge choosable.

# Proof.

We proceed by induction on the size $m$ of $G$. Since the result holds if $m=1$, the basis step for the induction is true. Assume that the statement of the theorem is true for all nonempty bipartite graphs of size less than $m$, where $m\ge 2$, and let $G$ be a nonempty bipartite graph of size $m$ on which is defined an edge coloring $c$ and where the numbers $\sigma_G(e)$, the sets $\mathfrak{L}(e)$ and the set $\mathfrak{L}$ are defined in the statement of the theorem.

Let $A$ be a set of edges of $G$. A matching $M\subseteq A$ is said to be **optimal** (in $A$) if the following is satisfied:

> For every edge $e\in A-M$, there is an edge $f\in M$ such that either
> (i) $u_e=u_f$ and $c(f)>c(e)$ or (ii) $w_e=w_f$ and $c(f)<c(e)$.

First, we show (by induction on the size of $A$) that for every $A\subseteq E(G)$, there is an optimal matching $M\subseteq A$.

Observe that if $A$ itself is a matching, then $M=A$ is vacuously optimal. If $|A|=1$, then $M=A$ is optimal and the basis step of this induction is satisfied.