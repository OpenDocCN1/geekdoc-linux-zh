# PROOF OF THEOREM 8.7

It follows from Theorem 8.3 that

$$ (1+x)(1+x^{2})(1+x^{3})...=\frac{1}{(1-x)(1-x^{2})(1-x^{3})...} $$

Hence

$$ \frac{1}{(1+x^{2})(1+x^{4})(1+x^{6})...(1-x)(1-x^{3})(1-x^{5})...} $$

$$ =\frac{1}{(1+x^{2})(1+x^{4})(1+x^{6})...}\times (1+x)(1+x^{2})(1+x^{3})... $$

$$ =(1+x)(1+x^{2})(1+x^{3})..., $$

which is the desired result.

We conclude this section with an identity due to Euler, who gave an algebraic proof of Theorem 8.8, for which we give a combinatorial proof. Exercise 8.1.3A(ii) shows that the generating function for the sequence $\{p_{h.o}(n)\}$ giving the number of partitions of $n$ into distinct odd parts is $(1+x)(1+x^{3})(1+x^{5}),...$. We can obtain another expres- sion for this generating function by analyzing the dot diagram for a partition of $n$ into distinct odd parts. We illustrate this by looking at the partition $26=13+7+5+1$. We represent this partition by a dot diagram where, instead of using rows of dots to represent the parts, we use symmetrical L-shaped arrays of dots, as shown on the left of Figure 8.5. The L shapes appear because we are considering partitions into $odd$ parts. We can split up the dot diagram on the left in the way shown in the middle diagram. In the bottom left-hand corner there is a $4\times 4$ array of dots. The dots to the right of this square, read in columns, form a partition of 5 into parts of size at most 4. The dots above the square, read in rows, form an identical partition, because of the symmetry. If we put these two identical partitions of 5 alongside one another, we get a partition of 10 into even parts of size at most 8, as shown on the right of Figure 8.5.

We now generalize this. Suppose we are given a partition of $n$ into unequal odd parts. We can represent this by an L-shaped array of dots. The bottom left-hand corner will form a square array of dots. If $k$ is the largest integer for which there is a square

![](bbox=[0.15, 0.88, 0.85, 0.98])

![](bbox=[0.15, 0.95, 0.28, 0.97])