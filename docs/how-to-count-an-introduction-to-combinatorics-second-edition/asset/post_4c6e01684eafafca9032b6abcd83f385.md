
## THEOREM 6.8

For all positive integers $n$, $p(2n) > p(1) + p(2) + ... + p(n)$.

### Proof

Clearly, if $k \leq n$, none of the dot diagrams for partitions of $k$ can have a row of dots with more than $n$ dots in it. Also, $2n - k \geq n$, and so, if we take $2n - k$ more dots, we can form a dot diagram for $2n$ by placing a row of $2n - k$ dots above the top row of the original dot diagram for $k$. This procedure associates, with each dot diagram for each $k$, where $k \leq n$, a dot diagram for $2n$. It is not difficult to check that all dot diagrams for $2n$ so obtained are different from one another, and we therefore see that there are at least $p(1) + p(2) + ... + p(n)$ of them. In addition, we have a dot diagram that consists of a single row of $2n$ dots that does not arise in this way. Hence $p(2n) > p(1) + p(2) + ... + p(n)$.

As a variant of Theorem 6.8, you might speculate from Tables 6.1 and 6.2 that, for all positive integers $n$, we have (i) $p(2n) \geq 2p(n)$ and (ii) $p(n + 2) \leq p(n + 1) + p(n)$. You are asked to show this in Exercise 6.4.4A. Furthermore, (ii) follows immediately from Theorem 8.6. Nevertheless, a similar proof of a lesser result is often of interest in mathematics, and here we can give such a proof using dot diagrams and a bit of ingenuity (which some might call “fiddling”). We have:

## THEOREM 6.9

For each positive integer $n$, $p(n + 2) \leq p(n + 1) + p(n)$.

### Proof

Let $D$ be the dot diagram for the partition $P$ of $n + 2$. We consider three distinct cases.

- a. $D$ contains at least one row containing just one dot. In this case we let $D'$ be the dot diagram obtained by deleting the bottom row of $D$ containing just one dot. Then $D'$ corresponds to a partition of $n + 1$.
- b. $D$ contains no rows containing just one dot but at least one row containing two dots. Suppose that the next smallest row contains $k$ dots, so that $k \geq 2$. We let $D'$ be the dot diagram obtained from $D$ by deleting the bottom row containing two dots and replacing the lowest row of $D$ by $k$ rows each containing one dot. Since $k \geq 2$, $D'$ corresponds to a partition of $n$ with more than one part of size 1.
- c. The smallest row of $D$ contains at least three dots. In this case we let $D'$ be the partition obtained from $D$ by deleting two dots from the bottom row of $D$. Then $D'$ corresponds to a partition of $n$ with at most one part of size 1.

Thus, in each case $D'$ corresponds to either a partition of $n + 1$ or of $n$. Also, if $D_1 \neq D_2$, then $D'_1 \neq D'_2$. This shows that there is a one-to-one correspondence between the partitions of $n + 2$ and some of the partitions of either $n$ or $n + 1$. Hence $p(n + 2) \leq p(n + 1) + p(n)$.

Note: Exercise 6.4.5B asks you to obtain, for all positive $n$, the lower bound $p(n + 2) \geq p(n + 1) + p(n) - p(n - 1)$. This and the intriguing “averaging” result in Exercise 6.4.5A, namely, \( p(n) \leq \frac{1}{2}(p(n + 1) + p(n - 1)) \), can be established using the following theorem.

## THEOREM 6.10

The number of partitions of \( n \) which have no parts of size 1 is \( p(n) - p(n - 1) \).

### Proof

Given a dot diagram, say \( D \), corresponding to a partition of \( n \) that has at least one part of size 1, we let \( D' \) be the dot diagram obtained by *removing* the bottom row consisting of a single dot. So \( D' \) corresponds to a partition of \( n - 1 \). Conversely, given a dot diagram corresponding to a partition of \( n - 1 \), by adding one row of just a single dot, we obtain a partition of \( n \) with at least one part of size 1. This shows that the partitions of \( n - 1 \) can be put in a one-to-one correspondence with the partitions of \( n \) that have at least one part of size 1. Thus, \( p(n) - p(n - 1) \) is the number of partitions of \( n \) with no parts of size 1.

As announced above, we shall return to partitions in Chapter 8 where we shall also describe a diagram-free way of discovering relationships between various partitions of integers.

# Exercises

- 6.4.1A Prove that for all positive integers \( k \) and \( n \) with \( 1 \leq k \leq n \), \( p(n) - p(n - 1) \leq p_{k}(n) + p(n - k) \).
- 6.4.1B Prove that for \( n \geq 2 \), \( p(n) - p(n - 2) \) is the number of partitions of \( n \) with at most one part of size 1. How may this result be generalized?
- 6.4.2A Prove that the number of partitions of \( n \) into *exactly* \( k \) parts is equal to the number of partitions of \( n \) whose maximum part has size *exactly* \( k \).
- 6.4.2B Prove that the number of partitions of \( n \) into *exactly* \( k \) parts is equal to the number of partitions of \( n + C(k, 2) \) into \( k \) *distinct* parts.
- 6.4.3A Show that the number of partitions of \( n \) into at most \( k \) parts is equal to the number of partitions of \( n + k \) into *exactly* \( k \) parts.
- 6.4.3B Show that, for all positive integers \( n \), \( k \), the number of partitions of \( 2n + k \) into exactly \( n + k \) parts is the same for each \( k \), namely, \( p(n) \).
- 6.4.4A Prove that, for every integer \( n \geq 2 \), \( p(2n) > 2p(n) \).
- 6.4.4B Is \( p(3n) > 3p(n) \) for all \( n > 1 \)?
- 6.4.5A Use Theorem 6.10 to prove that, for every positive integer \( n \), \( p(n) \leq \frac{1}{2}(p(n + 1) + p(n - 1)) \).
- 6.4.5B From numerical evidence it appears that, for all \( n \geq 2 \), \( p(n + 2) \geq p(n + 1) + p(n) - p(n - 1) \). Use Theorem 6.10 to confirm this.
- 6.4.6A Prove that, for \( n \geq 2 \), \( p(n) - p(n - 1) \) is the number of partitions of \( n \) whose two largest parts are equal.
- 6.4.6B Find (and prove) a similar formula for the number of partitions whose three largest parts are equal.

# Generating Functions and Recurrence Relations

## 7.1 FUNCTIONS AND POWER SERIES

In this chapter we describe a powerful algebraic technique that can be used to solve many combinatorial problems. We apply this technique to the solution of recurrence relations and especially to finding a succinct formula for the Fibonacci numbers (see Problem 7 of Chapter 1). In Chapter 8 this same technique is applied to investigate partitions of *n*. We saw a connection between algebra and counting in Chapter 2, where we gave a combinatorial proof of the binomial theorem. Recall that we did this by considering the terms that are obtained when the product

($a + b$) ($a + b$)...($a + b$)

with *n* terms is multiplied out in full. We can apply a similar idea in other contexts, as is shown by the following problem, which, though rather simple, will set us off in the right direction.

## **PROBLEM 7.1**

Consider the following product:

($1 + x + x^{2} + x^{3} + ...$)($1 + x^{2} + x^{4} + x^{6} + ...$). (7.1)

What is the coefficient of $x^{7}$ in this product?

### **Solution**

The coefficient of $x^{7}$ is 4 because when the terms in the first bracket are multiplied by those in the second bracket we obtain just four terms of degree seven, namely, $x \cdot x^{6}$, $x^{3} \cdot x^{4}$, $x^{5} \cdot x^{2}$, and $x^{7} \cdot 1$, or, as we now prefer to write them,

$x \cdot x^{6}$, $x^{3} \cdot x^{4}$, $x^{5} \cdot x^{2}$, $x^{7} \cdot x^{0}.$

These four terms correspond to the four different ways of writing 7 as the sum of two nonnegative integers, where the second is a multiple of 2, namely, 1 + 6, 3 + 4, 5 + 2, and 7 + 0. We can see, in general, that the coefficient of x^n in the product 7.1 is the number of ways of representing n as the sum of two nonnegative integers of which the second is even. Thus the coefficients give us an answer to a combinatorial problem. In fact, this problem is similar to the partition problems we have already discussed in Chapter 6. We return to this type of problem in Chapter 8. Meanwhile, the interest for us is the way we can use an infinite series to represent a sequence of numbers.

The above solution indicates that if $a_n$ is the number of ways of writing $n$ as the sum of two nonnegative integers of which the second is even, then

$$(1+x+x^2+x^3+...)(1+x^2+x^4+x^6+...)=\sum_{n=0}^{\infty} a_n x^n. \quad (7.2)$$

Equation 7.2 involves the sums of infinite series, and we have not yet said how these are to be interpreted. In fact, we can view the matter in two ways, algebraically and functionally. We could regard equations such as Equation 7.2 as dealing with formal algebraic expressions. The awkwardness of this approach arises when it comes to saying exactly what we mean by a formal algebraic expression. The coefficients in the series look like numbers, but what sort of animal is x?

It is tempting to say that x is a symbol, but then how can we combine a symbol with an abstract object like a number to form such things as 3x? In earlier days writers used to talk about “an indeterminate x” without ever really saying what this means. The modern approach, which aims to explain all mathematical concepts ultimately in terms of set theory, is to regard an algebraic expression such as

$$a_0+a_1 x+a_2 x^2+...$$

as simply a convenient way of representing the sequence of numbers

$$(a_0, a_1, a_2,...),$$

which is to be manipulated according to certain rules that arise from the algebraic background to this approach. The sequences are infinite if we are dealing with power series and finite if we are dealing with polynomials. There is, of course, no difficulty in defining what we mean by an infinite sequence in terms of sets. If X is a set, an infinite sequence of elements of X can be regarded as a function f: N→X. In this approach the rule for addition of sequences of numbers becomes

$$(a_0, a_1, a_2,...)+(b_0, b_1, b_2,...)=(a_0+b_0, a_1+b_1, a_2+b_2,...), \quad (7.3)$$

corresponding exactly to term-by-term addition of power series and polynomials. The multiplication rule for sequences is a little more complicated. If we multiply the terms in the series $a_0+a_1 x+a_2 x^2+...$ by those in the series $b_0+b_1 x+b_2 x^2+...$ and gather together terms of the same degree, we see that the coefficient of $x^n$ is

$$a_0 b_n+a_1 b_{n-1}+...+a_n b_0,$$
