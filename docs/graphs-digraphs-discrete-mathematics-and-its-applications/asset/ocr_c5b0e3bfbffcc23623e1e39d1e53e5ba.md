(b) Let $G$ be a graph of order $n$ having upper chromatic number $\overline{\chi}(G)$. Show that the domination number $\gamma(G)$ satisfies the inequality $\gamma(G) \cdot \overline{\chi}(G) \leq n$.

(c) Show that for every integer $k$, there exists a graph $G$ for which $\overline{\chi}(G)$ is defined and $\overline{\chi}(G) - \chi(G) = k$.

+   27. (a) Let $v$ be a vertex of a $k$-chromatic graph $G$ and let $U_1, U_2, \dots, U_\ell$ be the maximal independent sets of $G$ containing $v$. Prove that for some $k$-coloring of $G$, one of the resulting $k$ color classes is $U_i$ for some $i$ with $1 \leq i \leq \ell$.

(b) Let $G$ be a $k$-chromatic graph, $k \geq 2$, and $S$ an independent set of vertices in $G$. Prove that $\chi(G[\{V(G) - S\}]) = k-1$ if and only if $S$ is a color class in some $k$-coloring of $G$.

+   28. For a nonempty graph $G$, let $v$ be a vertex of $G$ and let $U_1, U_2, \dots, U_\ell$ be the maximal independent sets of $G$ containing $v$.

+   (a) Prove that $\chi(G) = 1 + \min_{1 \leq i \leq \ell} \chi(G[\{V(G) - U_i\}])$.

+   (b) What is the relationship between $\chi(G)$ and
+   $$1 + \max_{1 \leq i \leq \ell} \chi(G[\{V(G) - U_i\}])?$$

+   29. Prove that every Hamiltonian-connected graph of order at least 3 has chromatic number at least 3.

+   30. Determine (and prove) a necessary and sufficient condition for a connected graph to have a 2-colorable line graph.

+   31. Two dentists are having new offices designed for themselves. In the common waiting room for their patients, they have decided to have an aquatic area containing fish tanks. Because some fish require a coldwater environment while others are more tropical and because some fish are aggressive with other types of fish, not all fish can be placed in a single tank. It is decided to have ten exotic fish, denoted by $F_1, F_2, \dots, F_{10}$, where the fish that cannot be placed in the same tank as $F_i$ ($1 \leq i \leq 10$) are listed to the right of $F_i$.

|  |  |  |  |
| :--- | :--- | :--- | :--- |
| $F_1$: | $F_2, F_3, F_4, F_5, F_{10}$ | $F_2$: | $F_1, F_3, F_6$ |
| $F_3$: | $F_1, F_3, F_5$ | $F_3$: | $F_1, F_4, F_9$ |
| $F_7$: | $F_6, F_8, F_{10}$ | $F_8$: | $F_7, F_9, F_{10}$ |
| $F_{10}$: | $F_1, F_6, F_7, F_8, F_9$ |  |  |

|  |  |  |  |
| :--- | :--- | :--- | :--- |
| $F_3$: | $F_1, F_2, F_4$ |  |  |
| $F_6$: | $F_2, F_7, F_{10}$ |  |  |
| $F_9$: | $F_3, F_8, F_{10}$ |  |  |

What is the minimum number of tanks required?