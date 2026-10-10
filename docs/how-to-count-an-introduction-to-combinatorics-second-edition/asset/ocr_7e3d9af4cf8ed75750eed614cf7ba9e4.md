But is that all these *stirling numbers* are good for? By no means! Although the *stirling numbers*, $s(n,k)$, do not seem to occur as prominently in combinatorics as do the *Stirling numbers*, $S(n,k)$, they have some intimate connections with permutations, as shown below.

# ### Exercises

+   **5.1.1A** Write $[x]_k$ as a polynomial in $x.$
+   **5.1.1B** Write $[x]_r$ as a polynomial in $x.$

**5.1.2A** For each $n$ we let $P_i$ be the matrix $((−1)^{n−i}s(i, j))_{1≤i≤n, 1≤j≤n}$ made up of the coefficients in the polynomials $[x]_i$ for $1 ≤ i ≤ n,$ and let $Q_j$ be the matrix $(S(i,j))_{1≤i≤n, 1≤j≤n}$ of Stirling numbers. Thus from Tables 5.1 and 5.2 we see that $P_2 = \begin{pmatrix} 1 & 0 & 0 \\ -1 & 1 & 0 \\ 2 & -3 & 1 \end{pmatrix}, P_3 = \begin{pmatrix} 1 & 0 & 0 \\ -1 & 1 & 0 \\ 2 & -3 & 1 \end{pmatrix}, Q_2 = \begin{pmatrix} 1 & 0 & 0 \\ 1 & 1 & 0 \end{pmatrix}, Q_3 = \begin{pmatrix} 1 & 0 & 0 \\ 1 & 1 & 0 \\ 1 & 3 & 1 \end{pmatrix}.$ Check that $Q_2$ is the inverse of $P_2$ and that $Q_3$ is the inverse of $P_3.$

**5.1.2B** Using the same notation as in Exercise 5.1.2A, check that the matrix $Q_i$ is the inverse of the matrix $P_i.$

+   **5.1.3A** Show that, for each integer $n ≥ 1, s(n,1) = (−1)^{n−1}!$
+   **5.1.3B** Show that, for each integer $n ≥ 1, S(n,n−1) = [n(n−1)]/2 = s(n,n−1)$
+   **5.1.4A** Show that, for each integer $n ≥ 1, s(n,1) + s(n,2) + … + s(n,n) = n!$
+   **5.1.4B** Show that, for each integer $n > 1, s(n,1) − s(n,2) + … + (−1)^{n−1}s(n,n) = 0.

+   **5.1.5A** Show that, for all positive integers $k,$ $n, \sum_{r=1}^{n} \sum_{k=n−r}^{n} k! S(n,r) = n!C(k+n−1,n) = n!C(k+n−1,n).$
+   **5.1.5B** Show that, for all positive integers $k,$ $n, \sum_{r=1}^{n} (−1)^{r−1} r! S(n,r)C(k+r−1,n−1) = k^r.$
+   **5.1.6A** Show, directly from the definition, that, for all integers $k,$ $n,$ with $1 ≤ k ≤ n, s(n,k)$ is the sum of all the products of $n − k$ different integers taken from the set $\{1,2,…,n−1\}.$
+   **5.1.6B** Show by mathematical induction that for all integers $k, n,$ with $1 ≤ k < n,$ $S(n,k)$ is the sum of all products of $n − k$ integers taken from the set $\{1,2,…,k\}$ with repetitions allowed.
+   **5.1.7A** Let $\Theta$ be the operator of Problem 5.3. Find $\Theta^5$ in terms of the expressions $xD^k$ for $1 ≤ k ≤ 5,$ and verify that the coefficient of $xD^k$ is the Stirling number $S(5,k).$
+   **5.1.7B** Let $\Theta$ be the operator of Problem 5.3. Prove that, for each positive integer $n,$ $\Theta^n = \sum_{k=1}^{n} S(n,k)xD^k.$

# ## 5.2 PERMUTATIONS AND STIRLING NUMBERS

Recalling, from Chapter 2, how we expressed permutations as products of disjoint cycles, we begin with a simple definition.

**DEFINITION 5.2** For all integers $k, n$ with $1 ≤ k ≤ n,$ we let *Perm*$(n,k)$ be the set of permutations of the set $\{1,2,3,…,n\}$ made up of exactly $k$ disjoint cycles, and we let $p(n,k)$ be the number of permutations in *Perm* $(n,k),$ that is, $p(n,k) = \#$*Perm*$(n,k).$