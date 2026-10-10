# 15.2. THE PERFECT AND STRONG PERFECT GRAPH THEOREMS 403

Case 2. $v$ does not belong to any maximum clique of $G$. Suppose that $\chi(G) = \omega(G) = k$. Let there be given a $k$-coloring of $G$ using the colors $1, 2, \dots, k$. We may assume that $v$ is assigned the color 1. Let $V_{1}$ be the color class consisting of the vertices of $G$ that are colored 1. Thus, $v \in V_{1}$. Since $\omega(G) = k$, every maximum clique of $G$ must contain a vertex of each color. Since $v$ does not belong to a maximum clique, it follows that $|V_{1}| \geq 2$. Let $U_{1} = V_{1} - \{v\}$. Because every maximum clique of $G$ contains a vertex of $V_{1}$, it follows that $\omega(G-U_{1}) = \omega(G)-1 = k-1$. Since $G$ is perfect, $\chi(G-U_{1}) = k-1$. Let a $(k-1)$-coloring of $G-U_{1}$ be given, using the colors $1,2,\dots,k-1$. Since $V_{1}$ is an independent set of vertices, so is $U_{1} \cup \{v'\}$. Assigning the color $k$ to the vertices of $U_{1} \cup \{v'\}$ produces a $k$-coloring of $G'$. Therefore,

$\begin{equation*} k = \omega(G) \leq \omega(G') \leq \chi(G') \leq k \end{equation*}$

and so $\chi(G') = \omega(G')$.

It remains to show that $\chi(H) = \omega(H)$ for every induced subgraph $H$ of $G'$. This is certainly the case if $H$ is a subgraph of $G$. If $H$ contains $v'$ but not $v$, then $H \cong G'[V(H) - \{v'\} \cup \{v\}]$ and so $\chi(H) = \omega(H)$. If $H$ contains both $v$ and $v'$ but $H \not\cong G'$, then $H$ is the replication graph of $G'[V(H) - \{v'\}]$ and the argument used to show that $\chi(G') = \omega(G')$ can be applied to show that $\chi(H) = \omega(H)$.

As we observed following the proof of Theorem 14.24, the independence number of a graph equals the clique number of its complement.

# Theorem 15.10 (The Perfect Graph Theorem) A graph is perfect if and only if its complement is perfect.

Proof. Since $\overline{G} = \overline{G}$ for every graph $G$, it suffices to show that if $G$ is a perfect graph, then $\overline{G}$ is perfect. We proceed by induction on the order $n$ of a perfect graph $G$. For $n = 1$, $G = K_{1}$ which is perfect. Since $G = \overline{G}$, it follows that $\overline{G}$ is perfect and so the basis step of the induction is true. Assume, for an integer $n \geq 2$, that the complement of every perfect graph of order less than $n$ is perfect. Let $G$ be a perfect graph of order $n$. We show that $\overline{G}$ is perfect, that is, $\chi(F) = \omega(F)$ for every induced subgraph $F$ of $G$.

For each proper induced subgraph $F$ of $G$, there is a proper induced sub-graph $H$ of $G$ such that $H = \overline{F}$. Since $G$ is perfect, $H$ is perfect. It follows by the induction hypothesis that $F$ is perfect and so $\chi(F) = \omega(F)$. Hence, it remains to show that $\chi(\overline{G}) = \omega(\overline{G})$. Since $\chi(\overline{G}) \geq \omega(\overline{G})$, we need only show that

$\begin{equation} \chi(\overline{G}) \leq \omega(\overline{G}). \end{equation}$

Let $\mathcal{S}$ be the set consisting of all vertex sets of cliques of $G$. Consequently, if $U \in \mathcal{S}$, then $U$ is an independent set of vertices in $\overline{G}$. Let $\mathcal{T}$ be the set of all maximum independent sets in $G$. Hence, if $W \in \mathcal{T}$, then $|W| = \alpha(G)$. We claim that there exists some set $U \in \mathcal{S}$ having the property that

$\begin{equation} U \cap W \neq \emptyset \text{ for every } W \in \mathcal{T}. \end{equation}$