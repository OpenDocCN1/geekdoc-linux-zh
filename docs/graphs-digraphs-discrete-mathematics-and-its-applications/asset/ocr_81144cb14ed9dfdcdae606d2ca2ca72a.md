# Section 7.4

33. See the tournaments below.

![](bbox=[0.16, 0.23, 0.42, 0.38])

![](bbox=[0.45, 0.23, 0.72, 0.38])

+   35. If $D$ is an $n$-regular tournament of order $n$, then $n=2r+1$.
+   37. If $\overline{T}$ is not transitive, then $\overline{T}$ contains a triangle $(S_{1}, S_{2}, S_{3}, S_{1})$. Consider $v_{i} \in V(S_{i})$ for $i=1,2,3$.
+   39. (b) and (c) are score sequences of tournaments.
+   41. The tournament $T$ is the transitive tournament of order $n$.
+   43. (a) One. (b) Suppose that there is a tournament that contains three vertices not having both positive outdegree and positive indegree. (c) None.
+   45. Consider a shortest $u-v$ path.
+   47. Consider the set of vertices to which $v$ is adjacent.
+   49. Consider the sets of vertices to which $u$ is adjacent and from which $u$ is adjacent.
+   51. Assume that $(u, v) \in E(T)$ and then consider the set of vertices to which $v$ is adjacent.

# Section 7.5

+   53. Note that every vertex of maximum outdegree in a tournament is a king.
+   55. Let $T$ be the tournament with $V(T)=\{u, v, w, x\}$ and $E(T)=\{(v, u),(u, w),(u, x),(w, v),(w, x)\}$.
+   57. Assume that $n \geq 6$ is even. One possible construction of $T$: Let $T_{n-3}$ be a regular tournament of order $n-2$. Then the tournament $T$ of order $n$ has $V(T)=\{v_{1}, v_{2}, v_{3}\} \cup V\left(T_{n-3}\right)$ and $E(T)=\{(v_{1}, v_{2}), (v_{2}, v_{3}), (v_{3}, v_{1})\} \cup E\left(T_{n-3}\right) \cup E_{1} \cup E_{2} \cup E_{3}$ where $E_{1}=\{(v, v_{1}): v \in E\left(T_{n-3}\right)\}$, $E_{2}=\{(v, v_{2}): v \in E\left(T_{n-3}\right)\}$ and $E_{3}=\{(v_{3}, v): v \in E\left(T_{n-3}\right)\}$.

# Section 7.6

+   59. If $T$ is strong, then $T$ is Hamiltonian. If $T$ is not strong, then $T$ contains at least two strong components, at least one of which is nontrivial.
+   61. The strong component $S_{2}$ has $k / 15$ Hamiltonian paths.
+   63. (a) and (b). Both statements are false.
+   65. There must be a strong component of order $k$, another strong component of order $k-1$ or $k$ and $k$ trivial strong components. So: $n \geq k+(k-1)+k=3k-1$.