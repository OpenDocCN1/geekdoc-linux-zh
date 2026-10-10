Given any dot diagram $D$, we use $D'$ for its *dual dot diagram* formed from $D$ by writing the rows (columns) of dots in $D$ as the corresponding columns (rows) of $D'$. Similarly, for each partition $\pi$ of $n$, we let $\pi^c$ be its dual. In transposing the rows and columns, the number of dots does not change, so $\pi^c$ is also a partition of $n$. Usually, but not always, $\pi^c$ will be different from $\pi$. Note also that, for each partition $\pi$, the partition $\pi^c$, that is, the dual of its dual, is identical with $\pi$.

# PROOF OF THEOREM 6.1

Let $S$ be the set of all partitions of $n$ into at most $k$ parts, and let $T$ be the set of all partitions of $n$ with parts with size at most $k$. Now suppose $\pi$ is a partition in $S$. Since $\pi$ is a partition of $n$ into at most $k$ parts, there are at most $k$ rows in its dot diagram, $D$. Hence in the dual dot diagram, $D'$, each row contains at most $k$ dots. Therefore the dual partition $\pi^c$ is a partition of $n$ into parts of size at most $k$. Thus $\pi^c \in T$. Clearly, the converse also holds, so $\pi \in S$ if and only if $\pi^c \in T$. Thus $\pi \to \pi^c$ is a mapping from $S$ to $T$. This mapping is surjective (onto), since for $\pi \in T$, we have $\pi^c \in S$ and $\pi^{cc} = \pi$. Also, it is injective (one–one) as $\pi^c = \rho^c$ implies $\pi = \rho$, that is, $\pi = \rho$. Therefore, the mapping $\pi \to \pi^c$ is a bijection between $S$ and $T$. Hence $\#(S) = \#(T)$, that is, $p_k(n) = q_k(n)$.

The next result, making typical use of the dot diagram method, plays a role in eventually suggesting a rough lower bound for the size of $p_k(n)$. Note that conventions that $p_k(n) = 0$ and $p_k(0) = 1$ mean that we do not need to exclude the cases where $k = 1$ and $k = n$.

# THEOREM 6.2

If $k, n$ are positive integers with $k \leq 1$, then $p_k(n) = p_{k-1}(n) + p_k(n-k)$.

The proof can be followed without the need of a diagram. Nevertheless, there is no harm in offering a helpful picture, so we have included Figure 6.3.

# Proof

We divide the set, say $S$, of those partitions of $n$ that have at most $k$ parts into two subsets. Let $S_1$ be the set of partitions of $n$ into fewer than $k$ parts, and let $S_2$ be the set of the partitions of $n$ into exactly $k$ parts. Clearly, each partition in $S$ is in either $S_1$ or $S_2$ but not both. Therefore, $\#(S) = \#(S_1) + \#(S_2)$. Now, $S_1$ is the set of partitions of $n$ into at most $k-1$ parts. Hence $\#(S_1) = p_{k-1}(n)$.

Each partition in $S_2$ has a dot diagram with at least one dot in each of the $k$ rows. So if we remove one dot from each row, we obtain the dot diagram corresponding to a partition of $n-k$ into at most $k$ parts. Conversely, suppose we are given a dot diagram for a partition of $n-k$ into at most $k$ parts, then, by placing a column of $k$ dots on the left, we obtain a partition of $n$ into exactly $k$ parts. This is illustrated in Figure 6.3. It follows that $\#(S_2) = p_k(n-k)$.

We therefore have that $p_k(n) = \#(S) = \#(S_1) + \#(S_2) = p_{k-1}(n) + p_k(n-k)$.

We can extend Theorem 6.2 in the following way.