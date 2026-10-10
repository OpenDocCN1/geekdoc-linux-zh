# Exercises for Chapter 7

# Section 7.1. Introduction to Digraphs

+   1. (a) We saw in Theorem 1.14 that there exists no graph whose vertices have distinct degrees. Show that there exists a digraph of order 5 whose vertices have distinct outdegrees and distinct indegrees.
+   (b) Does there exist a digraph of order 5 whose vertices have distinct outdegrees but the same indegree?

+   2. Determine all digraphs of order 4 and size 4.

+   3. Show that for every positive integer $k$, there exists a digraph of even order, half of whose vertices have outdegree $a$ and half have outdegree $b$ and $a - b = k$.

+   4. If all vertices of a digraph $D$ of order 5 have distinct outdegrees except for two vertices that have the same outdegree $a$, then what are the possible values of $a$?

+   5. Prove or disprove: No digraph contains an odd number of vertices of odd outdegree or an odd number of vertices of odd indegree.

+   6. Prove or disprove: If $D_1$ and $D_2$ are two digraphs with $V(D_1)=\{u_1, u_2, \dots, u_n\}$ and $V(D_2)=\{v_1, v_2, \dots, v_n\}$ such that $\text{id}_{D_1}u_i = \text{id}_{D_2}v_i$ and $\text{od}_{D_1}u_i = \text{od}_{D_2}v_i$ for $i=1,2,\dots,n$, then $D_1 \cong D_2$.

+   7. Prove that there exist regular tournaments of every odd order but there are no regular tournaments of even order.

+   8. Let $T$ be a tournament with $V(T)=\{v_1, v_2, \dots, v_n\}$. We know that $$\sum_{i=1}^{n}\text{od}v_i=\sum_{i=1}^{n}\text{id}v_i=\binom{n}{2}$$ .
+   (a) Prove that $\sum_{i=1}^{n}(\text{od}v_i)^2 = \sum_{i=1}^{n}(\text{id}v_i)^2$.
+   (b) Prove or disprove: $\sum_{i=1}^{n}(\text{od}v_i)^3 = \sum_{i=1}^{n}(\text{id}v_i)^3$.

+   9. The **adjacency matrix** $A(D)$ of a digraph $D$ with $V(D)=\{v_1, v_2, \dots, v_n\}$ is the $n \times n$ matrix $[a_{ij}]$ defined by $a_{ij}=1$ if $(v_i, v_j) \in \vec{E}(D)$ and $a_{ij}=0$ otherwise.
+   (a) What information do the row sums and column sums of the adjacency matrix of a digraph provide?
+   (b) Characterize matrices that are adjacency matrices of digraphs.

+   10. (a) Prove Theorem 7.2: If $D$ is a digraph such that $\text{od}\,v \geq k \geq 1$ for every vertex $v$ of $\vec{D}$, then $D$ contains a cycle of length at least $k+1$.