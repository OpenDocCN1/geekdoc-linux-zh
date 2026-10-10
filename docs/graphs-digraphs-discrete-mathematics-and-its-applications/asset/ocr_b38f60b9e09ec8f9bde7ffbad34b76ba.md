# 21.1. THE PROBABILISTIC METHOD

If $X_{1}, X_{2}, \ldots, X_{k}$ are random variables on a probability space $S$ and $X = X_{1}+X_{2}+\cdots+X_{k}$, then it follows from the definition of expectation that $E[X] = \sum_{i=1}^{k} E[X_{i}]$. This property is often referred to as linearity of expectation.

Finally, if $E[X]=t$ for a random variable $X$ on a probability space $S$, then there are elements $s_{1}, s_{2}\in S$ for which $X(s_{1})\geq t$ and $X(s_{2})\leq t$. This observation is useful in many proofs involving the expected value of a random variable.

# Hamiltonian Paths in Tournaments

In Theorem 7.23, we saw that every tournament contains a Hamiltonian path. In what may be considered the first use of the probabilistic method, Tibor Szekely [231] showed, for every positive integer $n$, the existence of a tournament of order $n$ with many Hamiltonian paths. This result was stated without proof as Theorem 7.25 and is now proved as Theorem 21.3. The linearity of expectation is important in this proof, as is the idea of indicator random variables.

**Theorem 21.3** *For every positive integer* $n$, *there exists a tournament of order* $n$ *containing at least* $nl/2^{n-1}$ *Hamiltonian paths.*

**Proof.** Let $S$ be the probability space consisting of the $2^{\binom{n}{2}}$ different labeled tournaments with vertex set $\{v_{1}, v_{2}, \ldots, v_{n}\}$. The probabilities are defined by setting
$$ P([v_{i}, v_{j}]\in E(T))= P([v_{j}, v_{i}]\in E(T))=\frac{1}{2} $$
for each pair $v_{i}, v_{j}$ of distinct vertices of $T$ and letting these events be mutually independent. Each of the $2^{\binom{n}{2}}$ tournaments, then, is equally likely with probability $(\frac{1}{2})^{\binom{n}{2}}$.

Let $X$ be the random variable on the probability space $S$ that gives the number of Hamiltonian paths in a tournament $T$. In addition, for each of the $n!$ permutations $\sigma$ of $V(T)$, let $X_{\sigma}$ be the **indicator random variable** that depends on whether $\sigma$ gives a Hamiltonian path in $T$, that is, $X_{\sigma}=1$ if $\sigma$ describes a Hamiltonian path in $T$ and $X_{\sigma}=0$, otherwise. Then $P[X_{\sigma}=1] = (\frac{1}{2})^{n-1}$ since each of the $n-1$ arcs in the potential Hamiltonian path must be directed consistently. Thus,

$$E[X_{\sigma}]= 0 \cdot P[X_{\sigma}=0]+ 1 \cdot P[X_{\sigma}=1] = \left(\frac{1}{2}\right)^{n-1}. $$

Furthermore, $X=\sum X_{\sigma}$ where the sum is taken over all permutations $\sigma$ of $V(T)$. Therefore,
$$ E[X]= E\left[\sum X_{\sigma}\right]=\sum E[X_{\sigma}]= \frac{n!}{2^{n-1}}. $$