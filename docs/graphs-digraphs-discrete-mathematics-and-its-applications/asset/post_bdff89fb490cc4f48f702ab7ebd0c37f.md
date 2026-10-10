
and letting these events be mutually independent. Then each of the $2^n$ pairs $L_0, L_1$ is equally likely with probability \( \frac{1}{2^n} \).

For each $v \in U_i$ where $i = 0,1$,

$$
P[L_i \cap L(v)= \emptyset] \; = \; \binom{|L(v)|}{2} \; = \; \binom{1}{2}^{[2 \log_2 r]} \\ \leq \; \left( \binom{1}{2} \right)^{2 \log_2 r} \; = \; \frac{1}{r^2} \; \leq \; \frac{1}{2r}.
$$

where the last inequality follows since $r \geq 3$. For each vertex $v$ of $K_{r,r}$, let $A_v$ denote the event that $L_i \cap L(v) = \emptyset$ for $i = 0,1$. Then $P[A_v] < \frac{1}{2r}$ for every vertex $v$ of $K_{r,r}$. Now, consider the event $\bigcup A_v$, where the union is taken over all vertices $v$ of $K_{r,r}$. Then

$$
P\left[ \bigcup A_v \right] \leq \sum P[A_v] < 2r \left( \frac{1}{2r} \right) = 1.
$$

Since $P[\bigcup A_v] < 1$, it follows that $P\left[ \bigcup \overline{A_v} \right] > 0$, that is, $P\left[ \overline{\bigcap A_v} \right] > 0$. Hence, $\bigcap \overline{A_v} \neq \emptyset$ and so some element of the probability space $S$ belongs to $\bigcap \overline{A_v}$. Such an element is therefore a pair $L_0,L_1$ of subsets of $L$ that satisfies (21.5) and (21.6).

Theorem 21.2 can be proved without using probabilistic techniques (see Exercise 2), as could Theorem 21.1 (see Theorem 20.7). Both can be established using counting. However, in most important applications of the probabilistic methods, tools of probability are essential and proofs without them are unknown or very difficult. The last three results in this section involve some aspects of probability beyond counting.

## Random Variables

By a **random variable** $X$ on a probability space $S$, we mean a real-valued function on $S$. **The expected value** $E[X]$ of $X$ is the weighted average

$$
E[X] = \sum_{s \in S} X(s) \cdot P[s].
$$

We write ":X = k" to denote the event consisting of all elements of $S$ where the random variable $X$ has the value $k$. Consequently, it follows that

$$
E[X] = \sum k P[X = k],
$$

where the sum is taken over all possible values $k$ of $X$. It is the second expression for $E[X]$ described in (21.7) that will be most convenient to use.

If $X_{1}, X_{2}, \ldots, X_{k}$ are random variables on a probability space $S$ and $X = X_{1}+X_{2}+\cdots+X_{k}$, then it follows from the definition of expectation that $E[X] = \sum_{i=1}^{k} E[X_{i}]$. This property is often referred to as linearity of expectation.

Finally, if $E[X]=t$ for a random variable $X$ on a probability space $S$, then there are elements $s_{1}, s_{2}\in S$ for which $X(s_{1})\geq t$ and $X(s_{2})\leq t$. This observation is useful in many proofs involving the expected value of a random variable.

## Hamiltonian Paths in Tournaments

In Theorem 7.23, we saw that every tournament contains a Hamiltonian path. In what may be considered the first use of the probabilistic method, Tibor Szekely [231] showed, for every positive integer $n$, the existence of a tournament of order $n$ with many Hamiltonian paths. This result was stated without proof as Theorem 7.25 and is now proved as Theorem 21.3. The linearity of expectation is important in this proof, as is the idea of indicator random variables.

**Theorem 21.3** *For every positive integer* $n$, *there exists a tournament of order* $n$ *containing at least* $nl/2^{n-1}$ *Hamiltonian paths.*

**Proof.** Let $S$ be the probability space consisting of the $2^{\binom{n}{2}}$ different labeled tournaments with vertex set $\{v_{1}, v_{2}, \ldots, v_{n}\}$. The probabilities are defined by setting
$$ P([v_{i}, v_{j}]\in E(T))= P([v_{j}, v_{i}]\in E(T))=\frac{1}{2} $$
for each pair $v_{i}, v_{j}$ of distinct vertices of $T$ and letting these events be mutually independent. Each of the $2^{\binom{n}{2}}$ tournaments, then, is equally likely with probability $(\frac{1}{2})^{\binom{n}{2}}$.

Let $X$ be the random variable on the probability space $S$ that gives the number of Hamiltonian paths in a tournament $T$. In addition, for each of the $n!$ permutations $\sigma$ of $V(T)$, let $X_{\sigma}$ be the **indicator random variable** that depends on whether $\sigma$ gives a Hamiltonian path in $T$, that is, $X_{\sigma}=1$ if $\sigma$ describes a Hamiltonian path in $T$ and $X_{\sigma}=0$, otherwise. Then $P[X_{\sigma}=1] = (\frac{1}{2})^{n-1}$ since each of the $n-1$ arcs in the potential Hamiltonian path must be directed consistently. Thus,

$$E[X_{\sigma}]= 0 \cdot P[X_{\sigma}=0]+ 1 \cdot P[X_{\sigma}=1] = \left(\frac{1}{2}\right)^{n-1}. $$

Furthermore, $X=\sum X_{\sigma}$ where the sum is taken over all permutations $\sigma$ of $V(T)$. Therefore,
$$ E[X]= E\left[\sum X_{\sigma}\right]=\sum E[X_{\sigma}]= \frac{n!}{2^{n-1}}. $$

Since the expected value of the number of Hamiltonian paths is $n! / 2^{n-1}$, at least one tournament of order $n$ has at least $n! / 2^{n-1}$ Hamiltonian paths.

In the proof of Theorem 21.3, we define $n!$ indicator random variables $X_{\sigma}$ for the particular purpose of calculating the expected value $E[X]$ of $X = \sum X_{\sigma}$, where the sum is taken over all $n!$ permutations $\sigma$ of $V(T)$. These random variables are called indicator random variables because they indicate whether a permutation $\sigma$ describes a Hamiltonian path in $T$. Furthermore, $X = \sum X_{\sigma}$ gives the number of Hamiltonian paths in $T$.

In general, if $X$ is a random variable on a probability space $S$ that counts substructures (such as Hamiltonian paths in a random tournament), then $X$ can often be written as a sum of indicator random variables. These indicator random variables take on values in $\{0, 1\}$, where a value of $1$ indicates that one of the possible substructures occurs. The value of using an indicator random variable $X_{\ell}$ is that $E[X_{\ell}] = 0 \cdot P[X_{\ell} = 0] + 1 \cdot P[X_{\ell} = 1] = P[X_{\ell} = 1]$. The linearity of expectation therefore simplifies calculating $E[X]$.

## Domination

In Theorem 12.18, an upper bound for the domination number of a graph $G$ was given in terms of the order and minimum degree of $G$. This result is due to Vladimír Amtautov [7] and, independently, to Charles Rayan [183]. We now present a proof of this theorem using the probabilistic method.

The proofs of Theorems 21.4 and 21.5 include many approximating inequalities to determine bounds on probabilities under consideration. The proofs of the next two theorems will make use of the inequality $1 - p < e^{-p}$ for each real number $p$ with $p \in (0, 1)$, stated in (21.1).

**Theorem 21.4** If $G$ is a graph of order $n$ and $\delta(G) \geq 2$, then
$$
\gamma(G) \leq \frac{n(1 + \ln(\delta(G) + 1))}{\delta(G + 1)}.
$$

**Proof.** Let $\delta = \delta(G)$ and $p = \frac{\ln(\delta + 1)}{\delta + 1}$. Thus, $0 < p < 1$. Consider the probability space $S$ whose elements are the $2^n$ subsets of $V(G) = \{v_1, v_2, \ldots, v_n\}$. For a set $U$ of vertices of $G$, probabilities are assigned by defining $P[v_i \in U] = p$ and then letting these events be mutually independent. For a set $U \subseteq V(G)$, let $Y_U$ be the set of vertices of $G$ not in $U$ that have no neighbors in $U$, that is, let $Y_U = \{w \in V(G) - U : N(w) \cap U = \emptyset\}$. Then $U \cup Y_U$ is a dominating set of $G$. We next show that
$$
E[|U| + |Y_U|] \leq \frac{n(1 + \ln(\delta + 1))}{\delta + 1}.
$$
Certainly, the expected value $E[|U|]$ of $|U|$ is $np$. The random variable $|Y_U|$ is the sum $\sum_{v \in V(G)} X_v$ of indicator variables $X_v$, where $X_v = 1$ if and only if $v$ and all its neighbors are *not in* $U$. Since deg $v$ is at least $\delta(G)$ for each vertex $v$, it follows that
$P[X_v = 1] \le (1 - p)^{\deg v + 1} \le (1 - p)^{\delta + 1}.$

By the linearity of expectation,

$E[|Y_U|] = \sum_{v \in V(G)} E[X_v] \le n(1 - p)^{\delta + 1}.$

Since $(1 - p)^{\delta + 1} \le e^{-p(\delta + 1)}$, we have

$E[|U| + |Y_U|] \le np + n e^{-p(\delta + 1)} = \frac{n(1 + \ln(\delta + 1))}{\delta + 1}$

since $p = \frac{\ln(\delta + 1)}{\delta + 1}$. Thus, there is a set $U$, corresponding to $Y_U$, for which $U \cup Y_U$ is a dominating set of order at most $\frac{n(1 + \ln(\delta + 1))}{\delta + 1}$ and so $\gamma(G) \le \frac{n(1 + \ln(\delta + 1))}{\delta + 1}$.

One new idea was involved in the proof of Theorem 21.4. Consider the random variable $|U|$ on the $2^n$ subsets $U$ of $V(G)$. As we noted, $E[|U|]$ equals $np$, that is, $E[|U|] = \frac{n \ln(\delta + 1)}{\delta + 1}$. Consequently, there is a set $U \subseteq V(G)$ for which $|U| \le \frac{n \ln(\delta + 1)}{\delta + 1}$. However, $U$ need not be a dominating set. The set $U$ was then altered (in this case, by adding $Y_U$) to obtain the desired dominating set. The proof of Theorem 21.5 below employs the same technique of alteration. This proof also uses an inequality due to the Russian mathematician Andrey Markov.

Markov's inequality states that for a random variable $X$ on a probability space $S$ and positive number $t$,

$P[X \ge t] \le \frac{E[X]}{t}.$  (21.8)

As expected, "$X \ge t$" is used to denote the event consisting of all elements of $S$ where the random variable $X$ has value at least $t$. Markov's inequality will be employed in the next section for the case when $t = 1$, giving $P[X \ge 1] \le E[X]$.

## Chromatic Number and Girth

It was proved in Theorem 15.1 that there exists a triangle-free $k$-chromatic graph for every positive integer $k$. Furthermore, our next theorem, due to Erdős [79] and Lovász [158], which generalizes this result, was stated as Theorem 15.2 without proof.

Recall that $\alpha(G)$ denotes the (vertex) independence number of a graph $G$ and $g(G)$ denotes the girth of $G$.

**Theorem 21.5** For every two integers $k \ge 2$ and $\ell \ge 3$, there exists a graph $G$ with $\chi(G) = k$ and $g(G) > \ell$.
