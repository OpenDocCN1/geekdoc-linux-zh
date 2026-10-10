If there is a set $U \in \mathcal{S}$ satisfying property (15.2), then

$$\omega(\overline{G}-U)=\alpha(G-U)=\alpha(G)-1=\omega(\overline{G})-1.$$ 

It then follows by the induction hypothesis that

$$\chi(\overline{G}) \leq \chi(\overline{G}-U)+1=\omega(\overline{G}-U)+1=\omega(\overline{G}).$$  (15.3)

We now show that there is a set $U \in \mathcal{S}$ satisfying property (15.2). Assume, to the contrary, that no set $U \in \mathcal{S}$ satisfies (15.2). Then, for every set $U \in \mathcal{S}$, there is some set $W_U \in \mathcal{T}$ such that $|U \cap W_U| \neq 0$.

For each $x \in V(G)$, let $n_x = |\{U \in \mathcal{S}: x \in W_U\}|$. Next, we construct a new graph $G'$ from $G$. First, every vertex $x$ of $G$ for which $n_x = 0$ is removed from $G$. If $n_x > 0$, then $x$ is replaced in $G$ by a complete graph $G_x$ of order $n_x$. If $x$ and $y$ are two adjacent vertices of $G$, then every vertex of $G_x$ is joined to every vertex of $G_y$. The graph $G'$ is then defined by

$$V(G')=\bigcup_{x \in V(G)} V(G_x),$$

where $uv$ is an edge of $G'$ if and only if $u \in V(G_x)$ and $v \in V(G_y)$ such that either $x=y$ or $xy \in E(G)$.

Let $H = G[\{x \in V(G): n_x > 0\}]$. Since $H$ is an induced subgraph of the perfect graph $G$, it follows that $H$ is perfect. Since the graph $G'$ can be obtained from $H$ by a sequence of vertex replacements, it follows by Theorem 15.9 that $G'$ is perfect and so

$$\chi(G') = \omega(G').$$ (15.4)

First, we consider $\omega(G')$. By the construction of $G'$, every maximal complete subgraph of $G'$ has the form $G'[\cup_{x \in X} V(G_x)]$ for some $X \in \mathcal{S}$. So there exists a set $Y \in \mathcal{S}$ such that

$$\begin{aligned} \omega(G') &= \sum_{y \in Y} n_y = \sum_{y \in Y} \{U \in \mathcal{S}: y \in W_U\} \\ &= \sum_{U \in \mathcal{S}} |Y \cap W_U|. \end{aligned}$$

Since $G[Y]$ is complete in $G$ and $W_U$ is an independent set in $G$, it follows that $|Y \cap W_U| \leq 1$ for all $U \in \mathcal{S}$. Furthermore, it follows by our assumption that $|Y \cap W_Y| = 0$. Therefore,

$$\omega(G') \leq |\mathcal{S}| - 1.$$ (15.5)

Next, we consider $\chi(G')$. Observe that

$$\begin{aligned} |V(G')| &= \sum_{x \in V(G)} n_x = \sum_{x \in V(G)} \{U \in \mathcal{S}: x \in W_U\} \\ &= \sum_{U \in \mathcal{S}} |W_U| = |\mathcal{S}|\alpha(G). \end{aligned}$$