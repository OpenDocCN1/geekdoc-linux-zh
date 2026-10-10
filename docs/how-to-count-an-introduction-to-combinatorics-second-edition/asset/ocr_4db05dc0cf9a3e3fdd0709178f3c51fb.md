# **THEOREM 2.9**

For each positive integer $r$, the product of any $r$ consecutive positive integers is divisible by $r!$

# **Proof**

We need to prove that for all positive integers $k$, $r$ the product of the $r$ consecutive integers $k$, $k + 1$, $k + 2$,...,$k + r-1$ is divisible by $r$. Now,

```
$$\frac{k(k+1)(k+2)...(k+r-1)}{r!}=C(k+r-1,r),$$
```

by Theorem 2.3. Since this binomial coefficient gives the number of $r$-element subsets of a set of $k + r-1$ elements, it must be an integer. So $k(k + 1)(k + 2)$...$(k + r-1)$ is divisible by $r!$

# *Exercises*

**2.3.1A** A mathematics course offers students the choice of three options from 12 courses in pure mathematics, two options from 10 courses in applied mathematics, two options from 6 courses in statistics, and one option from 4 courses in computing. In how many different ways can the students choose their eight options?

**2.3.1B** A cricket squad consists of six batsmen, eight bowlers, three wicketkeepers, and four all-rounders. The selectors wish to pick a team made up of four batsmen, four bowlers, one wicketkeeper, and two all-rounders. How many different teams can they pick?

The next three pairs of questions can all be answered by using the binomial theorem. However, you are encouraged to give combinatorial proofs in the style of those we have given for the theorems in this section.

+   **2.3.2A** Prove that a set of $n$ elements has $2^{n}$ different subsets, and deduce that for each positive integer $n$, $\sum_{r=0}^{n}C(n,r) = 2^{n}$. 
+   **2.3.2B** Prove that, for each positive integer $n$, $\sum_{r=0}^{n}C(n,r)^{2} = C(2n,n)$.

+   **2.3.3A** Prove that, for all positive integers $n, k, s$ with $s \leq k \leq n$, $C(n,k)\ C(k,s) = C(n,s)\ C(n-s,k-s)$. 
+   **2.3.3B** Let $X$ be a finite set. Prove that the number of subsets of $X$ that contain an even number of elements is equal to the number of subsets of $X$ that contain an odd number of elements. Deduce that for each positive integer $n$, $\sum_{r=0}^{n}(-1)^{r}C(n,r) = 0$.

+   **2.3.4A** Prove that, for each positive integer $n$, $\sum_{r=0}^{n}rC(n,r) = n2^{n-1}$. 
+   *[Hint: Let X be an n-element set. Note that as X has C(n, r) subsets containing r elements, \sum_{r=0}^{n}rC(n,r)=\sum_{A\subseteq X}\sharp(A). Also, we can calculate \sum_{A\subseteq X}\sharp(A) by pairing off each subset A of X with its complement X\A. How many pairs are there, and what is \sharp(A)+\sharp(X\A)?]*

+   **2.3.4B** Prove that for each positive integer $n$, $\sum_{r=0}^{n}r^{2}C(n,r) = n(n + 1)2^{n-2}$. 
+   *[Hint: First find \sum_{r=0}^{n}r(r-1)C(n,r) by counting the ordered pairs (a, b), where a and b are chosen from an n-element set, in two ways. Then use the result of Exercise 2.3.4A.]*