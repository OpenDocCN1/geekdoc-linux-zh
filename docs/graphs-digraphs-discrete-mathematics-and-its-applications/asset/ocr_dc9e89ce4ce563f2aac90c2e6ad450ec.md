# 14.3. BOUNDS FOR THE CHROMATIC NUMBER

This, however, contradicts the fact that $\delta(\bar{G}) \geq n-p$. Thus, as claimed, the minimum degree of every subgraph of $\bar{G}$ is at most $n-p-1$. By Theorem 14.19, $\chi(\bar{G}) \leq 1+(n-p-1) = n-p$ and so

$$\chi(G)+\chi(\bar{G}) \leq (1+p)+(n-p) = n+1.$$ 
This verifies the upper bound in (i). By (14.3),

$$\chi(G) \cdot \chi(\bar{G}) \leq \left(\frac{n+1}{2}\right)^2,$$

verifying the final inequality.
$lacksquare$

As the proof of Theorem 14.23 indicates, the key inequality of the four inequalities listed is $\chi(G)+\chi(\bar{G}) \leq n+1$. Bonnie M. Steward [226] and Hans-Joachim Finck [90] showed that no improvement in Theorem 14.23 is possible.

# Theorem 14.24
Let $n$ be a positive integer. For every two positive integers $a$ and $b$ such that

$$2\sqrt{n} \leq a+b \leq n+1 \text{ and } n \leq ab \leq \left(\frac{n+1}{2}\right)^2$$ 
there is a graph $G$ of order $n$ such that $\chi(G)=a$ and $\chi(\bar{G}) = b$.

Proof.
Let $n_1, n_2, \ldots, n_a$ be $a$ positive integers such that $\sum_{i=1}^a n_i = n$ and $n_1 \leq n_2 \leq \ldots \leq n_a = b$. Since $a+b-1 \leq n \leq ab$, such integers $n_i$ ($1 \leq i \leq a$) exist. The graph $G = K_{n_1, n_2, \ldots, n_a}$ has order $n$ and $\bar{G} = K_{n_1} + K_{n_2} + \cdots + K_{n_a}$. Hence, $\chi(G) = a$ and $\chi(\bar{G}) = b$.
$lacksquare$

Of the several bounds for the chromatic number of a graph $G$, the clique number $\omega(G)$ is the best known and simplest lower bound for $\chi(G)$, while $1+\Delta(G)$ is the best known and simplest upper bound for $\chi(G)$. If $\Delta(G) \geq 3$ and $G$ is not complete, then $\Delta(G)+1$ is an improved upper bound for $\chi(G)$ by Brooks' theorem (Theorem 14.21). Bruce Reed [198] conjectured that $\chi(G)$ is always at least as close to $\omega(G)$ as to $1+\Delta(G)$.

# Reed's Conjecture
For every graph $G$,

$$\chi(G) \leq \frac{\omega(G)+1+\Delta(G)}{2}.$$ 
As we saw in Theorem 14.9, for a graph $G$ of order $n$, the number $n-\alpha(G)+1$ is also an upper bound for $\chi(G)$. By Theorem 14.16, $(n+\omega(G))/2$ is also an upper bound for $\chi(G)$. The following improved upper bound for $\chi(G)$ is due to Robert C. Brigham and Ronald D. Dutton [36].

# Theorem 14.25
For every graph $G$ of order $n$,

$$\chi(G) \leq \frac{\omega(G)+n+1-\alpha(G)}{2}.$$