Case 2. The color lists in $\mathfrak{L}$ are not all the same. Then there are adjacent vertices $v_i$ and $v_{i+1}$ in $G$ such that $L(v_i) \neq L(v_{i+1})$. Thus there exists a color $a \in L(v_{i+1}) - L(v_i)$. The graph $C_n - v_i$ is a path of order $n-1$. Let $\mathfrak{L}' = \{L(v) : v \in V(C_n - v_i)\}$. By Theorem 15.14, there exists an $\mathfrak{L}'$-list-coloring $c'$ of $C_n - v_i$ in which $c'(v_{i+1}) = a$. Let $b \in L(v_i)$ such that $b \neq c'(v_{i-1})$. Then the coloring $c$ defined by

$c(v) = \begin{cases} b & \text{if } v = v_i \\ c'(v) & \text{if } v \neq v_i \end{cases}$

is an $\mathfrak{L}$-list-coloring of $G$.

**Corollary 15.17** *For every even integer* $n \ge 4$, $\chi_\ell(C_n) = 2$.

Since the chromatic number of every odd cycle is 3, the list chromatic number of every odd cycle is at least 3. Indeed, every odd cycle is 3-choosable (see Exercise 28).

We have seen that all trees and even cycles are 2-choosable. Of course, these are both classes of bipartite graphs. Not every bipartite graph is 2-choosable, however. To illustrate this, we consider $\chi_\ell(K_{3,3})$, where $K_{3,3}$ is shown in Figure 15.10(a). By Theorem 15.13, $\chi_\ell(K_{3,3}) \le 1 + \Delta(K_{3,3}) = 4$. In fact, $\chi_\ell(K_{3,3}) \le 3$, as we next show. Let there be given lists $L(v_i)$, $1 \le i \le 6$, where $|L(v_i)| = 3$. We consider two cases.

Case 1. *Some color occurs in two or more of the lists* $L(v_1)$, $L(v_2)$, $L(v_3)$ *or in two or more of the lists* $L(v_4)$, $L(v_5)$, $L(v_6)$, *say color* $a$ *occurs in* $L(v_1)$ *and* $L(v_2)$. Then assign $v_1$ and $v_2$ the color $a$ and assign $v_5$ any color in $L(v_5)$. Then there is an available color in $L(v_i)$ for $v_i$ ($i = 4, 5, 6$).

Case 2. *The lists* $L(v_1)$, $L(v_2)$, $L(v_3)$ *are pairwise disjoint as are the lists* $L(v_4)$, $L(v_5)$, $L(v_6)$. Let $a_1 \in L(v_1)$ and $a_2 \in L(v_2)$. If none of the lists $L(v_4)$, $L(v_5)$, $L(v_6)$ contain both $a_1$ and $a_2$, then let $a_3$ be any color in $L(v_3)$. Then there is an available color for each of $v_4$, $v_5$, $v_6$ to construct a proper coloring of $K_{3,3}$. If exactly one of the lists $L(v_4)$, $L(v_5)$, $L(v_6)$ contains both $a_1$ and $a_2$, then select a color $a_3$ in $L(v_3)$ so that none of $L(v_4)$, $L(v_5)$, $L(v_6)$ contains all of $a_1$, $a_2$, $a_3$. By assigning $v_3$ the color $a_3$, we see that there is an available color for each of $v_4$, $v_5$, and $v_6$.

Hence, as claimed, $\chi_\ell(K_{3,3}) \le 3$. We show, in fact, that $\chi_\ell(K_{3,3}) = 3$. Consider the sets $L(v_i)$, $1 \le i \le 6$, shown in Figure 15.10(b). Assume, without loss of generality, that $v_1$ is colored 1. Then $v_4$ must be colored 2 and $v_5$ must be colored 3. Whichever color is chosen for $v_3$ is the same color as that of either $v_4$ or $v_5$. This produces a contradiction. Hence, $K_{3,3}$ is not 2-choosable and so $\chi_\ell(K_{3,3}) = 3$. The graph $G = K_{3,3}$ shows that it is possible for $\chi(G) > \chi_\ell(G)$. In fact, $\chi_\ell(G)$ can be considerably larger than $\chi(G)$.

**Theorem 15.18** *If* $r$ *and* $k$ *are positive integers such that* $r \ge {2k-1 \choose k}$, *then*

$\chi_\ell(K_{r,r}) \ge k + 1$.