Proof. We have already noted that if G is P_3-decomposable, then G has even size. For the converse, assume that G has even size. Suppose first that G is Eulerian, where the edges of G are encountered in the order e_1, e_2, ..., e_m. Then each of the sets {e_1, e_2}, {e_3, e_4}, ..., {e_{m-1}, e_m} induces a copy of P_3, so G is P_3-decomposable. Otherwise, G has 2k odd vertices for some k \geq 1. By Theorem 5.3, E(G) can be partitioned into subsets E_1, E_2, ..., E_k, where for each i, G[E_i] is an open trail T_i of even length connecting odd vertices of G. (That is, G can be decomposed into k open trails of even length connecting odd vertices.) Then, as with the Eulerian circuit above, the edges of each trail T_i can be paired off so that each pair of consecutive edges on each trail induce a copy of P_3. Thus, G is P_3-decomposable.

Many theorems and conjectures dealing with decompositions involve H-decompositions for some graph H. Richard Wilson [258] proved that for every graph H without isolated vertices, there exist infinitely many positive integers n such that K_n is H-decomposable.

# Theorem 13.12 Let H be a graph of size m without isolated vertices and let

d = gcd{deg v : v \in V(H)}.

Then there exists a positive integer N such that whenever (i) n \geq N, (ii) m | (n \choose 2) and (iii) d | (n - 1), then K_n is H-decomposable.

There is a conjecture involving decompositions of a different nature [2].

# The Ascending Subgraph Decomposition Conjecture Every graph of size (k+1 \choose 2) for some positive integer k has a decomposition D = {G_1, G_2, ..., G_k} where G_i has size i for 1 \leq i \leq k and G_i is isomorphic to a subgraph of G_{i+1} for i = 1, 2, ..., k - 1.

To illustrate the Ascending Subgraph Decomposition Conjecture, we consider the graph G = C_5 \square K_2 of size 15 = (6 \choose 2) = \sum_{i=1}^{5} i, shown in Figure 13.8. The decomposition D = {G_1, G_2, G_3, G_4, G_5}, also drawn in this figure, shows that this conjecture holds for this graph G. While this conjecture has been verified for many classes of graphs, very little of a general nature is known.

# 13.3 Cycle Decomposition

As we have noted, the vast majority of factorization and decomposition conjectures and results deal with factoring or decomposing complete graphs into a specific graph or graphs. A problem of particular interest concerns determining those complete graphs that are K_3-decomposable or, equivalently, C_3-decomposable. This problem has a curious history.