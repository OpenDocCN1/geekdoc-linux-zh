# 3.3. SPANNING TREES

$A=\begin{bmatrix} 3 & -1 & -2 \\ 1 & 2 & -3 \\ -4 & -1 & 5 \end{bmatrix}$

$A'=\begin{bmatrix} 3 & -1 \\ 1 & 2 \end{bmatrix} \quad (-1)^{3+3} \det(A')=3(2)-(-1)1=7$

$A''=\begin{bmatrix} 1 & -3 \\ -4 & 5 \end{bmatrix} \quad (-1)^{1+2} \det(A'')=-[1(5)-(-3)(-4)]=5$

![](bbox=[0.35, 0.32, 0.65, 0.35])

# Theorem 3.26 (The Matrix-Tree Theorem) If $G$ is a nontrivial labeled graph with adjacency matrix $A$ and degree matrix $D$, then the number of distinct spanning trees of $G$ is the value of any cofactor of the matrix $D-A$.

Proof. Let $V(G)=\{v_1, v_2, \ldots, v_n\}$. First, observe that the row sum of row $i$ (or column sum of column $i$) in $A$ is $\operatorname{deg} v_i$, so every row sum or column sum of $D-A$ is 0. Consequently, the cofactors of $D-A$ have the same value.

Assume first that $G$ is a disconnected graph. Of course in this case, $G$ has no spanning trees. Let $G_1$ be a component of $G$ and suppose that $V(G_1)=\{v_1, v_2, \ldots, v_r\}$, where $1 \leq r < n$. Let $M$ be the $(n-1) \times (n-1)$ submatrix of $D-A$ obtained by deleting row $n$ and column $n$ from $D-A$. Since the sum of the first $r$ rows of $M$ is the zero vector of length $n-1$, the rows of $M$ are linearly dependent and so $\det(M)=0$, as desired.

Henceforth, we assume that $G$ is a connected graph of order $n$ and size $m$ where $E(G)=\{e_1, e_2, \ldots, e_m\}$. Thus $m \geq n-1$. Let $C=\{c_{ij}\}$ be an $n \times m$ matrix where $c_{ij}=1$ or $c_{ij}=-1$ if $v_i$ is incident with $e_j$ and such that each column has one entry that is $1$ and one entry that is $-1$, while all other entries in the column are 0. We show that for the transpose $C^t$ of $C$, we have $C \cdot C^t=D-A$. The $(i, j)$-entry of $C \cdot C^t$ is

$\sum_{k=1}^m C_{ik} C_{jk}$

which has the value $\operatorname{deg} v_i$ if $i=j$, the value $-1$ if $i \neq j$ and $v_i v_j \in E(G)$ and the value 0 if $i \neq j$ and $v_i v_j \notin E(G)$. Hence, as claimed, $C \cdot C^t=D-A$.

Consider a spanning subgraph $H$ of $G$ containing $n-1$ edges of $G$. Let $C'$ be the $(n-1) \times (n-1)$ submatrix of $C$ determined by the column labels associated with the edges of $H$ and by all rows of $C$ with one exception, say row $k$.

We now determine the absolute value $|\det(C')|$ of the determinant of $C'$. If $H$ is disconnected, then $H$ has a component $H_i$ not containing $v_k$. The sum of the row vectors of $C'$ corresponding to the vertices of $H_i$ is the zero vector of length $n-1$. Hence the row vectors in $C'$ are linearly dependent and so $|\det(C')|=0$.