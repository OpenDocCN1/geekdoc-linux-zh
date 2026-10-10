On the other hand, if $e \in A - M$, then $a \in L(e)$. Since $M$ is optimal in $A$, there is an edge $f \in M$ such that either (i) $u_e = u_f$ and $c(f) > c(e)$ or (ii) $u_e = w_f$ and $c(f) < c(e)$. Thus,

$$ \begin{equation*} \mid L^{\prime}(e)\mid = \mid L(e)\mid - 1 = \sigma_G(e) - 1 \geq \sigma_{G^{\prime}}(e). \end{equation*} $$

Let $\mathfrak{L}^{\prime} = \{ L^{\prime}(e) : e \in E(G^{\prime}) \}$. Since the size of $G^{\prime}$ is less than that of $G$, it follows by the induction hypothesis that $G^{\prime}$ is $\mathfrak{L}^{\prime}$-edge choosable. Thus, there exists a proper edge coloring $c^{\prime} : E(G^{\prime}) \to \mathbb{N}$ of $G^{\prime}$ such that $c^{\prime}(e) \in L^{\prime}(e)$ for every edge $e$ of $G^{\prime}$. Define $c : E(G) \to \mathbb{N}$ by

$$ \begin{equation*} c(e) = \left\{ \begin{array}{cl} c^{\prime}(e) & \text{if } e \in E(G^{\prime}) \ a & \text{if } e \in M. \end{array} \right. \end{equation*} $$

Then $c(e) \in L(e)$ for every edge $e$ of $G$ and $c(e) \neq c(f)$ for every two adjacent edges $e$ and $f$ of $G$. Hence, $c$ is a proper edge coloring and $G$ is $\mathfrak{L}$-edge choosable.

From Lemma 18.16, we can now present a proof of Galvin’s theorem.

# **Theorem 18.17 (Galvin’s Theorem)** If $G$ is a bipartite graph, then

$$ \begin{equation*} \chi^{\prime}_{\ell}(G) = \chi^{\prime}(G). \end{equation*} $$

**Proof.** Since $G$ is bipartite, it follows by König’s theorem (Theorem 17.7) that $\chi^{\prime}(G) = \Delta(G) = \Delta$. Thus, there exists a proper edge coloring $c : E(G) \to \{1, 2, \ldots, \Delta\}$. For each edge $e$ of $G$, let $L(e)$ be a list of colors such that

$$ \begin{align*} \mid L(e)\mid &= \sigma_G(e) = 1 + \mid \{ f \in E(G) : u_e = u_f \text{ and } c(f) > c(e) \} \mid \ &\qquad + \mid \{ f \in E(G) : w_e = w_f \text{ and } c(f) < c(e) \} \mid \ &\leq 1 + (\chi^{\prime}(G) - c(e)) + (c(e) - 1) = \chi^{\prime}(G). \end{align*} $$

Let $\mathfrak{L} = \{ L(e) : e \in E(G) \}$. By Lemma 18.16, $G$ is $\mathfrak{L}$-edge choosable. Therefore, $G$ is $\chi^{\prime}(G)$-edge choosable and so $\chi^{\prime}_{\ell}(G) \leq \chi^{\prime}(G)$. Since $\chi^{\prime}(G) \leq \chi^{\prime}_{\ell}(G)$, we have the desired result.

Since every bipartite graph is of Class one, it follows that the list chromatic index of every bipartite graph $G$ equals $\Delta(G)$.

# ## 18.3 Total Colorings

We now consider colorings that assign colors to both the vertices and the edges of a graph. A **total coloring** of a graph $G$ is an assignment of colors to the vertices and edges of $G$ such that distinct colors are assigned to (1) every two adjacent vertices, (2) every two adjacent edges and (3) every incident vertex and edge. A **$k$-total coloring** of a graph $G$ is a total coloring of $G$ from a set of $k$ colors. A graph $G$ is **$k$-total colorable** if there is a $k$-total coloring of $G$.