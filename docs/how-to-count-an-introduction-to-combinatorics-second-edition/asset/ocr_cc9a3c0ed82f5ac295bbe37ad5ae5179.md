$$1 + p(1)x + p(2)x^2 + p(3)x^3 + \dots = \frac{1}{(1-x)(1-x^2)(1-x^3)\cdots}\quad\quad (8.9)$$

It follows from Equation 8.9 that

$$(1 + p(1)x + p(2)x^2 + p(3)x^3 + \dots)((1-x)(1-x^2)(1-x^3)\dots) = 1.$$

And hence, by Equation 8.8,

$$(1 + p(1)x + p(2)x^2 + p(3)x^3 + \dots)(1 - x - x^2 + x^5 + x^7 - x^{12} - x^{15} + x^{22} + x^{36} - \dots) = 1.\quad\quad (8.10)$$

Now, equating the coefficients of $x^n$ in Equation 8.10, we have

$$
\begin{aligned}
&p(n) - p(n-1) - p(n-2) + p(n-5) + p(n-7) - p(n-12) - p(n-15) \\
&+ p(n-22) + p(n-26) - \cdots = 0,
\end{aligned}
$$
and hence we obtain the formula of Theorem 8.6.

The recurrence relation given by Theorem 8.6 can be used to determine, reasonably quickly and by pencil and paper, the values of $p(n)$, at least for modest-sized values of $n$.

# **PROBLEM 8.4**

In Chapter 6, we obtained the values of $p(n)$ for $0 \leq n \leq 10$ as given in Table 8.1.\*
Use Theorem 8.6 to evaluate $p(n)$ for $11 \leq n \leq 15$.

TABLE 8.1

| $n$  | $p(n)$ |
|:-----|:-------|
| 0 | 1 |
| 1 | 1 |
| 2 | 2 |
| 3 | 3 |
| 4 | 5 |
| 5 | 7 |
| 6 | 11 |
| 7 | 15 |
| 8 | 22 |
| 9 | 30 |
| 10 | 42 |

> \* The comment after Theorem 6.3 explains why we take the value of $p(0)$ to be 1. The other values are taken from Table 6.1.