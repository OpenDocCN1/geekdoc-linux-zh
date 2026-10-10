As an illustration of Theorem 7.17, we consider the sequence

$\pi: 1, 2, 2, 3, 3, 4.$

In this case, $s_n$ (actually $s_6$) has the value 4; thus, we delete the last term, repeat the first $s_n = 4$ terms, and subtract 1 from the remaining terms, obtaining

$\pi_1': 1, 2, 2, 3, 2.$

Rearranging, we have

$\pi_1: 1, 2, 2, 2, 3.$

Repeating this process twice more, we have

$\pi_2': : 1, 2, 2, 1$

$\pi_2: : 1, 1, 2, 2$

$\pi_3: : 1, 1, 1.$

The sequence $\pi_3$ is clearly a score sequence of a tournament. By Theorem 7.17, $\pi_2$ as well, as are $\pi_1$ and $\pi$. We can use this information to construct a tournament with score sequence $\pi$. The sequence $\pi_3$ is the score sequence of the tournament $T_3$ of Figure 7.17. Proceeding from $\pi_3$ to $\pi_2$, we add a new vertex to $T_3$ and join it to two vertices of $T_3$ and **from** the other, producing a tournament $T_2$ with score sequence $\pi_2$. To proceed from $\pi_2$ to $\pi_1$, we add a new vertex to $T_2$ and join it to vertices having scores 1, 2 and 2 and **from** the remaining vertices of $T_2$, producing a tournament $T_1$ with score sequence $\pi_1$. Continuing in the same fashion, we finally produce a desired tournament $T$ with score sequence $\pi$ by adding a new vertex to $T_1$ and joining it **to** vertices having scores 1, 2, 2 and 3, and joining it **from** the other vertex.

The sociologist Hymen Garslin Landau [152] characterized those sequences of nonnegative integers that are score sequences of tournaments. The proof we present of his theorem is due to Carsten Thomassen [233].

# Theorem 7.18 A nondecreasing sequence $\pi: s_1, s_2, \ldots, s_n$ of nonnegative integers is a score sequence of a tournament if and only if for each integer k with $1 \leq k \leq n$,

$$\sum_{i=1}^{k} s_i \geq \binom{k}{2},$$

with equality holding when $k = n$.

Proof. Suppose first that $\pi: s_1, s_2, \ldots, s_n$ is a score sequence of a tournament of order $n$. Then there exists a tournament $T$ with $V(T) = \{v_1, v_2, \ldots, v_n\}$ such that $\text{od}_T v_i = s_i$ for $i = 1, 2, \ldots, n$. For an integer $k$ with $1 \leq k \leq n$ and $S = \{v_1, v_2, \ldots, v_k\}$, the subdigraph $T_1 = T[S]$ induced by $S$ is a tournament of order $k$ and size $\binom{k}{2}$. Since $\text{od}_T v_i \geq \text{od}_{T_1} v_i$ for $1 \leq i \leq k$, it follows that

$$\sum_{i=1}^{k} s_i = \sum_{i=1}^{k} \text{od}_T v_i \geq \sum_{i=1}^{k} \text{od}_{T_1} v_i = \binom{k}{2}.$$