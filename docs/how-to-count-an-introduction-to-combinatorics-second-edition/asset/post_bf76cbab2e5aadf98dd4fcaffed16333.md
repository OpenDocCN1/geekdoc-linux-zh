
iii. This graph has two vertices of degree 3 ($c$ and $f$) with all the other vertices having degree 4. So it is semi-Eulerian. One example of a trail that includes all the edges is $c\rightarrow d \rightarrow e \rightarrow f \rightarrow a \rightarrow b \rightarrow c \rightarrow e \rightarrow a \rightarrow d \rightarrow b \rightarrow f$.

**9.6.2A** Let $G$ be a connected graph with just two vertices, say $a$ and $b$, whose degrees are odd numbers. Let $G'$ be the graph obtained from $G$ by adding an edge joining $a$ and $b$. This increases the degrees of $a$ and $b$ by 1 so every vertex of $G'$ has even degree. Therefore, by Theorem 9.9(a), $G'$ is Eulerian and so has a closed trail that includes every edge of $G'$. If we delete the added edge joining $a$ and $b$ from this closed trail, we obtain a trail that includes every edge of $G$. Hence $G$ is semi-Eulerian.

**9.6.3A** The graph has four vertices whose degrees are odd. We need to increase each of their degrees by 1 to make the graph Eulerian. So two more bridges are needed. These could correspond to the edges $ab$ and $cd$, or $ac$ and $bd$, or $ad$ and $bc$.

**9.7.1A** i. In the diagram below we have labeled the vertices so we can refer to them. This graph is Hamiltonian. For example, $a\rightarrow f\rightarrow e\rightarrow d\rightarrow c\rightarrow b\rightarrow h\rightarrow i\rightarrow j\rightarrow k\rightarrow l\rightarrow m\rightarrow g\rightarrow a$ is a Hamiltonian path in the graph (there are lots of others).

![](img/eb401bf41900fd678cd9d368a197e486_395_0.png)

ii. This graph is not Hamiltonian. An argument to show this is given below the diagram where we have labeled the vertices so that we can refer to them.

![](img/eb401bf41900fd678cd9d368a197e486_395_1.png)

The graph is bipartite with each edge joining a vertex in the set $V_{1}=\{a,c,f,g,k\}$ to a vertex in the set $V_{2}=\{b,c,d,h,i,j\}$. A Hamiltonian path would have to alternate between a vertex in $V_{1}$ and a vertex in $V_{2}$. This is impossible as there are more vertices in $V_{2}$ than in $V_{1}$. Hence there is no Hamiltonian path in this graph.

### **9.7.2A** The Petersen graph is not Hamiltonian. In the following argument to prove this we use the labeling of the vertices given in Figure 9.14. Please draw your own diagram.

We note first that since a Hamiltonian path must visit each vertex, and each vertex of the Petersen graph has degree three, a Hamiltonian path must use exactly two of the edges adjacent to each vertex. We note next that a Hamiltonian path must include at least one edge between a vertex in the set $\{a,b,c,d,e\}$ and a vertex in the set $\{f,g,h,i,j\}$. So, because of the symmetry of the graph, we may assume that any Hamiltonian path includes the edges $af$ and $ae$. It follows that the edge $ab$ is not included, and hence the edges $bc$ and $bg$ are used. We now consider which of the edges adjacent to $d$ are used.

If $de$ is used, then $ej$ cannot be used, and hence the edge $gj$ must be used. Since $bg$ and $gj$ are used, $gi$ is not used, and so $di$ and $fi$ are used. This means that we already have a closed path $a \to f \to j \to i \to d \to e \to a$ that does not include all the vertices. Thus a Hamiltonian path can not include the edge $de$. Similarly, the edge $cd$ cannot be used. But this is impossible as two edges adjacent to $d$ must be used. We deduce that there is no Hamiltonian path.

### **9.7.3A** Let $G$ be a graph with $n$ vertices and $\frac{1}{2}(n-1)(n-2)+2d$ edges, where $n \geq 3$. Suppose $u$ and $v$ are two vertices of $G$ not joined by an edge, and that $\delta(u)+\delta(v)=d$. Then there are at most $C(n-2,2)=\frac{1}{2}(n-2)(n-3)$ edges joining the $n-2$ vertices of $G$ other than $u$ and $v$, and there are $d$ edges joining these $n-2$ vertices to $u$ or $v$ both. So the total number of edges is at most $\frac{1}{2}(n-2)(n-3)+d$. Therefore $\frac{1}{2}(n-1)(n-2)+2d \leq \frac{1}{2}(n-2)(n-3)+d$ and hence $n \leq d$. It therefore follows from Theorem 9.10 that $G$ is Hamiltonian.

For each $n$ let $G_{n}$ be the graph obtained from the complete graph $K_{n-1}$ with $n-1$ vertices by adding one additional vertex $v$ that is joined to just one vertex of $K_{n-1}$. Then $G_{n}$ has $\frac{1}{2}(n-1)(n-2)+1$ edges but is not Hamiltonian as $v$ has degree 1.

### **9.7.4A** The graph is connected, and each vertex has an even degree. So, by Theorem 9.9, the graph is Eulerian. Any Hamiltonian path would have to include, for each vertex of degree 2, both edges adjacent to it. However, the six edges that are adjacent to the vertices of degree 2 form a closed path that does not go through all the other vertices. So there is not a Hamiltonian path. Hence the graph is not Hamiltonian.

### **9.8.1A** The graph can be colored using three colors. The vertices at the corners of the square can be colored the first color, the vertex at the center with a second color, and the other four vertices with a third color. As the graph includes three vertices each joined to the other two, it cannot be colored with fewer than three colors. So its chromatic number is 3.

**9.8.2A** i. Let $G$ be a connected planar graph with $v$ vertices and no vertices of degree less than 5. Suppose $G$ has $k$ vertices of degree 5, and hence $v-k$ vertices of degree at least 6, and that $G$ has $e$ edges. By Theorem 9.7, $e \leq 3v-6$, and by the handshaking lemma, $2e \geq 5k + 6(v-k) = 6v-k$. Therefore $6v-k \leq 2e \leq 6v-12$ and hence $12 \leq k$.

ii. A regular icosahedron has 12 vertices each of degree 5, and hence when projected onto the plane provides a graph with the required properties. It can be drawn as shown in the diagram below.

![](img/eb401bf41900fd678cd9d368a197e486_397_0.png)

**9.8.3A** In the graph shown below the vertices represent the subjects. They are joined by an edge if at least one student takes both subjects.

![](img/eb401bf41900fd678cd9d368a197e486_397_1.png)

Because the graph includes a triangle, at least three time slots are needed. If we assign a, c, and f to one hour; b, d, and g to a second hour; and e and h to a third hour, then vertices joined by an edge are assigned different hours. So three different hours are needed.

**9.8.4A**

![](img/eb401bf41900fd678cd9d368a197e486_397_2.png)

# CHAPTER 10

**10.1.1A** There is just one tree with two vertices, one with three vertices, two with four vertices, and three with five vertices, as shown below.

![](img/eb401bf41900fd678cd9d368a197e486_398_0.png)

![](img/eb401bf41900fd678cd9d368a197e486_398_1.png)

![](img/eb401bf41900fd678cd9d368a197e486_398_2.png)

![](img/eb401bf41900fd678cd9d368a197e486_398_3.png)

![](img/eb401bf41900fd678cd9d368a197e486_398_4.png)

**10.1.2A** We prove this result by mathematical induction. It is clearly true for a tree with two vertices. Suppose it is true for trees with $k$ vertices where $k \geq 2$. Now let $T$ be a tree with $k + 1$ vertices. $T$ is therefore a connected graph. A connected graph in which each vertex has degree at least 2 must have a closed path. By Theorem 9.5, $T$ must contain at least one vertex, say $v_0$, of degree 1. Let $T'$ be the graph obtained from $T$ by deleting $v_0$ and the edge adjacent to it. $T'$ will still be connected. Hence it is a tree with $k$ vertices, so by the induction hypothesis, it has at least two vertices of degree 1. At least one of these must also have degree 1 in the graph $T$. So $T$ has at least two vertices with degree 2. So the result holds also for trees with $k + 1$ vertices. So, by mathematical induction the result is true for all trees.

**10.1.3A** The two trees below each have degree sequences 1, 1, 2, 2, 3 but are clearly not isomorphic. (From the solution to Exercise 10.1.1A, we see that there are no examples with fewer than six vertices.)

![](img/eb401bf41900fd678cd9d368a197e486_398_5.png)

![](img/eb401bf41900fd678cd9d368a197e486_398_6.png)

**10.1.4A** Let $G$ be a graph with $n$ vertices, $n-1$ edges, and no closed paths, where $n \geq 3$. Suppose that $G$ has $k$ components with $n_1, n_2, ..., n_k$ vertices, respectively, with $k \geq 1$. So $n_1 + n_2 + ... + n_k = n$. The connected components have no closed paths, and hence are themselves trees. So by Theorem 10.1(b), the components have $n_1-1, n_2-1, ..., n_k-1$ edges, respectively. So $G$ has $(n_1-1) + (n_2-1) + ... + (n_k-1) = n - k$ edges. Since $G$ has $n - 1$ edges, $k = 1$, and hence $G$ is connected.

**10.1.5A** If $a_1, ..., a_n$ is the degree sequence for a tree, this tree has $n$ vertices, and so, by Theorem 10.1, it has $n - 1$ edges. Hence, by the handshaking lemma, $a_1 + ... + a_n = 2(n-1) = 2n-2$. We prove the converse by mathematical induction. If $a_1 + a_2 = 2$, where $a_1, a_2$ are positive integers, $a_1 = a_2 = 1$. Then, as 1,1 is the degree sequence of a tree, the result holds
