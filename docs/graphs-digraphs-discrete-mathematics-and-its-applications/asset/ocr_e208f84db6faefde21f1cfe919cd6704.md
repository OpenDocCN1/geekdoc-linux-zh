![](bbox=[0.26, 0.13, 0.76, 0.21])

Figure 12.1: Matchings and maximum matchings

If \( M \) is a matching in a graph \( G \), then every vertex of \( G \) is incident with at most one edge of \( M \). A vertex that is incident with no edges of \( M \) is referred to as an **M-unmatched vertex** or simply an **unmatched vertex** if the matching \( M \) is clear. The following theorem will prove to be useful.

**Theorem 12.1** *Let \( M_1 \) and \( M_2 \) be matchings in a graph \( G \). Then each component of the spanning subgraph \( H \) of \( G \) with* \( \mathrm{E}(H)=\left(M_1-M_2\right) \cup\left(M_2-M_1\right) *is one of the following:*
(i) *an isolated vertex,*

(ii) *an even cycle whose edges are alternately in \( M_1 \) and in \( M_2 \),*

(iii) *a nontrivial path whose edges are alternately in \( M_1 \) and in \( M_2 \) and such that each end-vertex of the path is either \( M_1 \)-unmatched or \( M_2 \)-unmatched but not both.*

**Proof.** First, we note that \( \Delta(H) \leq 2 \), for if \( H \) contains a vertex \( v \) such that \( \deg_H v \geq 3 \), then \( v \) is incident with at least two edges in the same matching. Since \( \Delta(H) \leq 2 \), every component of \( H \) is a path (possibly trivial) or a cycle. Since no two edges in a matching are adjacent, the edges of each cycle and path in \( H \) are alternately in \( M_1 \) and in \( M_2 \). Thus each cycle in \( H \) is even.

Suppose that \( e=wv \) is an edge of \( H \) and \( u \) is the end-vertex of a path \( P \) that is a component of \( H \). The proof will be complete once we have shown that \( u \) is \( M_1 \)-unmatched or \( M_2 \)-unmatched but not both. Since \( e \in E(H) \), it follows that \( e \in M_1-M_2 \) or \( e \in M_2-M_1 \). If \( e \in M_1-M_2 \), then \( u \in \) not \( M_1 \)-unmatched. We show that \( u \) is \( M_2 \)-unmatched. If this is not the case, then there are an edge \( f \in M_2 \) (thus \( f \neq e \)) such that \( f \) is incident to \( u \). Since \( e \) and \( f \) are adjacent, \( f \notin M_1 \). Thus, \( f \in M_2-M_1 \subseteq E(H) \). This, however, is impossible since \( u \) is the end-vertex of \( P \). Therefore, \( u \) is \( M_2 \)-unmatched. Similarly, if \( e \in M_2-M_1 \), then \( u \) is \( M_1 \)-unmatched.

# Augmenting Paths and Maximum Matchings