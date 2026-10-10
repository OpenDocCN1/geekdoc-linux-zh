# 11.2. THE GENUS OF A GRAPH

Let $G$ be a connected graph of order $n$ and size $m$ that is 2-cell embedded on $S_{k+1}$, resulting in $r$ regions. We may assume, without loss of generality, that no vertex of $G$ lies on any handle of $S_{k+1}$ and that the edges of $G$ are drawn on the handles so that a closed curve can be drawn around each handle that intersects no edge of $G$ more than once.

Let $H$ be one of the $k+1$ handles of $S_{k+1}$. There are necessarily edges of $G$ on $H$; for otherwise, the handle belongs to a region $R$ in which case any closed curve around $H$ cannot be continuously deformed in $R$ to a single point, contradicting the assumption that $R$ is a 2-cell. We now draw a closed curve $C$ around $H$, which intersects some edges of $G$ on $H$ but intersects no edge more than once. Suppose that there are $t \geq 1$ points of intersection of $C$ and the edges on $H$. At each point of intersection, a new vertex is introduced. Each of the $t$ edges then becomes two edges. Also, the segments of $C$ between vertices become edges. We add two vertices of degree 2 along $C$ to produce two additional edges. (This guarantees that the resulting structure will be a graph, not a multigraph.)

Let $G_1$ be the graph just constructed, where $G_1$ has order $n_1$, size $m_1$ and $r_1$ regions. Then

$n_1 = n + t + 2$ and $m_1 = m + 2t + 2$.

Since each portion of $C$ that became an edge of $G_1$ is in a region of $G$, the addition of such an edge divides that region into two regions, each of which is a 2-cell. Since there are $t$ such edges,

$r_1 = r + t$.

We now cut the handle $H$ along $C$ and “patch” the two resulting holes, producing two duplicate copies of the vertices and edges along $C$ (see Figure 11.16). Denote the resulting graph by $G_2$, which is now 2-cell embedded on a surface $S_k$.

![](bbox=[0.15, 0.72, 0.85, 0.85])

**Figure 11.16:** Converting a 2-cell embedding of $G_1$ on $S_{k+1}$ into a 2-cell embedding of $G_2$ on $S_k$

Let $G_2$ have order $n_2$, size $m_2$ and $r_2$ regions, all of which are 2-cells. Then

$n_2 = n_1 + t + 2$, $m_2 = m_1 + t + 2$ and $r_2 = r_1 + 2$.

Furthermore, $n_2 = n + 2t + 4$, $m_2 = m + 3t + 4$ and $r_2 = r + t + 2$. By the induction hypothesis, $n_2 - m_2 + r_2 = 2 - 2k$. Therefore,