parts, that is, partitions of $n$ in which there is at most one part of any given size, the generating function for the sequence \(\{p_n(n)\}\) is obtained by just taking, from each bracket \((1+x^3+x^{2k}+x^{3k}+\dots)\) of Equation 8.2, the terms $1$ and $x^k$, that is, those that correspond to having either no part of size $k$ or just one part of size $k$.

So to solve Problem 8 we only have to prove that the two generating functions of Lemma 8.2 are identical. Can that really be true? Yes! And the proof is as follows.

# **THEOREM 8.3**

For all positive integers $n, p_d(n) = p_o(n)$.

# **Proof**

Since $(1-x^{2i}) = (1+x^i)(1-x^i)$, it follows that $(1+x^i) = (1-x^{2i})/(1-x^i)$. Hence

```
$$\begin{aligned} p_d(x) = &(1+x)(1+x^2)(1+x^3)(1+x^4)(1+x^5)\dots \\ &= \frac{(1-x^2)(1-x^4)(1-x^6)(1-x^8)(1-x^{10})\dots}{(1-x)(1-x^2)(1-x^3)(1-x^4)(1-x^5)\dots}.\end{aligned}$$
```

Now, canceling each term in the numerator of this last expression with the identical term in the denominator leaves us just the terms \((1-x), (1-x^3), (1-x^5), \dots\) in the denominator, that is, the terms of the form \((1-x^{2t-1})\), where $t$ is a positive integer $t$. Thus

```
$$p_d(x)=\frac{1}{(1-x)(1-x^3)(1-x^5)\dots} = \prod_{i=1}^{\infty} \frac{1}{(1-x^{2i-1})} = p_o(x).\tag{8.5}$$
```

Since the generating functions for the two sequences \(\{p_d(n)\}\) and \(\{p_o(n)\}\) are identical, their coefficients must be equal. That is, for each positive integer $n$, we have $p_d(n) = p_o(n)$.

Note that we have proved Theorem 8.3 by establishing the algebraic identity given in Equation 8.5, which could be written as

```
$$(1+x)(1+x^2)(1+x^3)\dots = \frac{1}{(1-x)(1-x^3)(1-x^5)\dots}.\tag{8.6}$$
```

In the next section we come to a work saver!

# *Exercises*

+   **8.1.1A** Find the coefficient of $x^{100}$ in the following products.
+   i. \((1+x^7+x^{14}+x^{21}+\dots)(1+x^{11}+x^{22}+x^{33}+\dots)\)
+   ii. \((1+x^3+x^6+x^9+\dots)(1+x^{13}+x^{26}+x^{39}+\dots)\)

+   **8.1.1B** What is the coefficient of $x^{24}$ in the product
+   \((1+x^2)(1+x^3)(1+x^5)(1+x^7)(1+x^{11})(1+x^{13})(1+x^{17})(1+x^{19})?\)
+   Interpret the answer in terms of the partitions of 24.