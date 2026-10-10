To see that the bound $3n-5$ presented in Theorem 19.4 is sharp, observe that the complete 4-partite graph $K_{1,1,1,n-3}$ has order $n$ and size $3n-6$. Every cycle in $K_{1,1,1,n-3}$ contains at least two of the three vertices having degree $n-1$. Thus, no two cycles of $K_{1,1,1,n-3}$ are disjoint.

# Subgraphs with a Given Minimum Degree

Another example of a theorem in extremal graph theory gives the minimum number of edges that a graph $G$ of order $n$ must have to guarantee that $G$ contains a subgraph with a specified minimum degree.

**Theorem 19.5** Let $k$ and $n$ be integers with $1 \le k < n$. Every graph of order $n$ and size at least

$$(k-1)n-\binom{k}{2}+1$$

contains a subgraph with minimum degree $k$.

**Proof.** We proceed by induction on $n \ge k+1$. First, assume that $n=k+1$. Let $G$ be a graph of order $n$ and size at least

$$(k-1)n-\binom{k}{2}+1=(n-2)n-\binom{n-1}{2}+1=\binom{n}{2}.$$  (n-2)n - (n-1)2 + 1 = n2

Then $G=K_n=K_{k+1}$ and so $G$ itself is a graph with minimum degree $k$.

Assume that every graph of order $n-1 \ge k+1$ and size at least

$$(k-1)(n-1)-\binom{k}{2}+1$$

contains a subgraph with minimum degree $k$. Let $G$ be a graph of order $n$ and size $m$, where

$$m\ge (k-1)n-\binom{k}{2}+1.$$  (k-1)n - k2 + 1

We show that $G$ contains a subgraph with minimum degree $k$. If $G$ itself is not such a graph, then $G$ contains a vertex $v$ with $deg \, v \le k-1$. Then the order of $G-v$ is $n-1$ and its size is $m-\deg v$. Since

$$m-\deg v \ge (k-1)n-\binom{k}{2}+1-(k-1)=(k-1)(n-1)-\binom{k}{2}+1,$$

it follows by the induction hypothesis that $G-v$, and therefore $G$ as well, contains a subgraph with minimum degree $k$.  \blacksquare

The bound given in Theorem 19.5 cannot be improved. If $k=1$, then the graph $\overline{K_n}$ contains no subgraph with minimum degree 1. More generally, for $2 \le k < n$, the graph $\overline{K_{n-k+1}} \vee K_{k-1}$ has order $n$ and size $(k-1)n-\binom{k}{2}$