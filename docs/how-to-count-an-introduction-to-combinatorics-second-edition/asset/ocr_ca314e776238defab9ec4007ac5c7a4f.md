# **Proof**

We have seen that for all $n \geq 1$, $p(n,1) = (n-1)! = s(n,1)$. (See Exercise 5.1.3A and Problem 5.5.) Also, by Theorems 5.2 and 5.3, the numbers $s(n,k)$, $p(n,k)$ satisfy the same recurrence relation. It follows that for all integers $k$, $n$ with $1 \leq k \leq n$, $p(n,k) = s(n,k)$. Finally, for each positive integer $n$, $p(n,n) = 1 = s(n,n)$. Hence for all integers $k$, $n$, $1 \leq k \leq n$, $p(n,k) = s(n,k)$.

If you compare the entries in Tables 5.1 and 5.2 you will find that we always have $S(n,k) \leq s(n,k)$. Does this state of affairs persist? Theorem 5.5 shows that the answer is in the affirmative.

# **THEOREM 5.5**

For all integers $k$, $n$, such that $1 \leq k \leq n$, we have $S(n,k) \leq s(n,k)$.

# **Proof**

$S(n,k)$ is the number of partitions of the integers $\{1,2,3,...,n\}$ into $k$ disjoint, nonempty subsets. To each such partition $P = \{a_1,a_2,...,a_k\} \cup \{b_1,b_2,...,b_j\} \cup ... \cup \{z_{i_1}z_{i_2}...,z_i\}$, we associate the permutation $P'$ written in cycle notation as $a_{i_1}a_{i_2}...a_{i_k}(b_1b_2...b_j)...(z_{i_1}z_{i_2}...z_i)$. $P$ is a permutation of $\{1,2,3,...,n\}$ made up of exactly $k$ cycles, that is, $P \in \text{Perm}(n,k)$. The mapping $P \to P'$ is injective. It follows that $S(n,k) \#(\text{Perm}(n,k)) = s(n,k)$.

# **Exercises**

+   * **5.2.1A** Find a general formula for $p(n,n-2)$, with $n \geq 4$.
+   * **5.2.1B** Find general formulas for $p(n,n-3)$.
+   * **5.2.2A** Show that, for each integer $n > 1$, $0!S(n,1) - 1!S(n,2) + ... + (-1)^{n-1}(n-1)!S(n,n) = 0$.
+   * **5.2.2B** Show that, for all positive integers $k$, $n$, with $k \leq n$, $k^n = C(k,1)S(n,1)!! + C(k,2)S(n,2)!! + ... + C(k,k)S(n,k)!!$.
+   * **5.2.3A** Show that, for all positive integers $k$, $n$, with $k \leq n$, $\sum_{r=1}^{n} C(n,r)S(n,r) = S(n+1,k+1)$.
+   * **5.2.3B** Show that, for all positive integers $k$, $n$, with $k \leq n$, $\sum_{r=1}^{n} C(n,r)S(n,r) = s(n+1,k+1)$.

# **5.3 CATALAN NUMBERS**

Applying hindsight, we begin with a definition "out of the blue."

# **DEFINITION 5.3**

For each integer, $n \geq 0$, we define the *nth Catalan number* $c_n$ by

```
$$c_n = \frac{1}{n+1}C(2n,n).$$
```

These numbers are singled out because they occur in a large number of combinatorial problems. It is not immediately obvious that $C(2n,n)$ must be divisible by $n+1$. However, this follows from the alternative formula for $C_n$ given at the end of the proof of Theorem 5.6, and also from the result of Exercise 5.3.1A.