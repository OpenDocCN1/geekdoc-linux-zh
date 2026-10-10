+   
+   (a) For the graph $G$, $\chi(G)=\omega(G)$.
+   (b) The graph $G$ is perfect.
+   

23. Let $G$ be a graph where $v \in V(G)$.  According to Theorem 15.9, if $G$ is perfect, then the replication graph $R_v(G)$ is perfect.  Is the converse true?

24.  A **transitive orientation** of a graph $G$ is an orientation $D$ of $G$ such that whenever $(u, v)$ and $(v, w)$ are arcs of $D$, then so too is $(u, w)$.  If $G$ has a transitive orientation, then $G$ is called a **comparability graph**.

+   
+   (a) Show that every bipartite graph is a comparability graph.
+   (b) Show that every complete graph is a comparability graph.
+   (c) Show that every comparability graph is perfect.
+   (d) Use (a)-(c) to show that every bipartite graph and every complete graph is perfect.
+   (e) Give an example of a comparability graph that is neither complete nor bipartite.
+   

25. Let $G$ be a graph with $V(G)=\left\{v_1, v_2, \ldots, v_n\right\}$.  The **shadow graph** $\operatorname{Shad}(G)$ of $G$ is that graph with vertex set $V(G) \cup\left\{u_1, u_2, \ldots, u_n\right\}$, where $u_i$ is called the **shadow vertex** of $v_i$ and where $u_i$ is adjacent to both $u_j$ and $v_j$ if $v_i$ is adjacent to $v_j$ for $1 \leq i, j \leq n$.  How are $\omega(G)$ and $\omega(\operatorname{Shad}(G))$ related and how are $\chi(G)$ and $\chi(\operatorname{Shad}(G))$ related?

+   
+   (a) Show that if $G$ is perfect, then $|V(H)| \leq \alpha(H) \cdot \omega(H)$ for every induced subgraph $H$ of $G$ (see Theorem 15.11).
+   (b) Use Theorem 15.11 to prove the Perfect Graph Theorem (Theorem 15.10).
+   

# Section 15.3.  List Colorings

27. Use the greedy coloring algorithm to show that $\chi_{\ell}(G) \leq 1+\Delta(G)$ for every graph $G$.

28. Prove, without using Exercise 27, that every odd cycle is 3-choosable.

29. Prove that $\chi_{\ell}\left(K_{2,3}\right)=2$.

30. Prove that $\chi_{\ell}\left(K_{2,4}\right)=3$.

31. Prove that $\chi_{\ell}\left(K_{3,27}\right)>3$.

32. We have seen that $\chi_{\ell}\left(K_{3,3}\right)=3$.  By Theorem 15.18, $\chi_{\ell}\left(K_{10,10}\right)>3$.  Give a precise and detailed proof of this special case of Theorem 15.18.

33. Prove that the list-chromatic number of $P_n \square K_2$ is 3 for every integer $n \geq 4$.