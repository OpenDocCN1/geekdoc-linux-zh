A theorem by Hoffman and Singleton [129] states everything that is known about $r$-regular Moore graphs of girth 5.

# Theorem 19.12  *If G is an r-regular Moore graph (r ≥ 3) of girth 5, then r = 3, r = 7 or possibly r = 57.*

As we already noted, the 2-regular Moore graph of girth 5 is $C_{5}$, the 3-regular Moore graph of girth 5 is the Petersen graph and the 7-regular Moore graph of girth 5 is the Hoffman-Singleton graph. It is not known whether there is a 57-regular Moore graph of girth 5 but if such a graph does exist, its order must be 3250.

The definition of Moore graph has been extended to permit a Moore graph to have even girth. For every two adjacent vertices $u$ and $v$ in an $r$-regular graph $G$ of diameter $d$, the number of vertices $w$ in $G$ such that

$\min\{d(u,w), d(v,w)\} = i \text{ for } 0 \le i \le d-1$ is at most $2(r-1)^{i}$. Thus, the order of $G$ is at most

$2 + 2(r-1) + 2(r-1)^{2} + \cdots + 2(r-1)^{d-1}$.  (19.3)

An $r$-regular graph $G$ of diameter $d$ whose order is the expression in (19.3) is also called a **Moore graph**. Such a Moore graph $G$ necessarily has girth $g = 2d$. Hence,

$M(r,g) = M(r,2d) = 2\left[1 + (r-1) + (r-1)^{2} + \cdots + (r-1)^{d-1}\right].$

Thus, $n(r,g) = M(r,g)$. Therefore, in this case as well, a Moore graph is a cage. That is, if $G$ is an $r$-regular Moore graph of diameter $d$, then the girth of $G$ is $g = 2d$ and $G$ is an $(r,g)$-cage.

In the more general definition of Moore graphs that allows even girth, the graph $K_{r,r}$ is an $r$-regular Moore graph of girth 4, the Heawood graph is a 3-regular Moore graph of girth 6 and the Tutte-Coxeter graph is a 3-regular Moore graph of girth 8. More generally, Robert Mark Damerell [64] and Eiichi Bannai and Tatsuro Ito [12] verified that other than the Moore graphs already mentioned, a Moore graph must have girth 5, 6, 8 or 12. The following theorem summarizes the information concerning Moore graphs.

# Theorem 19.13  *There exists an r-regular Moore graph of odd girth g when*

+   - $g = 3$ and $r \geq 3$, in which case $K_{r+1}$ is the unique Moore graph;
+   - $g = 5$ and $r = 3$, in which case the Petersen graph is the unique Moore graph;
+   - $g = 5$ and $r = 7$, in which case the Hoffman-Singleton graph is the unique Moore graph; and
+   - possibly when $g = 5$ and $r = 57$.