# S$_6$

| Partition | Cycle Type | Number of this Type |
|---|---|---|
| 6 | x$_6$ | **120** |
| 5+1 | x$_5$x | 144 |
| 4+2 | x$_4$x$_2$ | 90 |
| 4+1+1 | x$_4$ x$_1$ | 90 |
| 3+3 | x$_3^2$ | 40 |
| 3+2+1 | x$_3$x$_2$x$_1$ | 120 |
| 3+1+1+1 | x$_3$x$_1^3$ | 40 |
| 2+2+2 | x$_2^3$ | 15 |
| 2+2+1+1 | x$_2^2$x$_1^2$ | 45 |
| 2+1+1+1+1+1 | x$_2$x$_1^5$ | 15 |
| 1+1+1+1+1+1+1 | x$_1^6$ | 1 |

Thus the cycle index of S$_6$ is

```
$$\frac{1}{720}\left( x_1^6 + 15 x_1^4 x_2 + 45 x_1^3 x_3 + 15 x_1^2 x_4 + 40 x_1^2 x_2 x_3 + 120 x_1 x_2 x_4 + 40 x_1 x_2^2 + 90 x_1^2 x_4 + 90 x_2 x_4 + 144 x_1 x_5 + 120 x_6 \right).$$
```

# 14.3.4A

In each case we use the formula in expression 14.7 for the number of permutations in S$_n$ that have a specified cycle type.

+   i. x$_2^3$x$_6$. Here, in the notation of expression 14.7, $t=2$, $k_1=2$, $r_1=3$, $k_2=6$, $r_2=1$. So the number of permutation of this type is $12!/(3!2^3 1! 6!)$ = 1,663,200.

+   ii. x$_1^4$ x$_3$x$_3$. There are $12!/(4! 1! 3! 1! 5!) = 1,330,560$ permutations of this type.

+   iii. x$_3$x$_2^2$ x$_3$ x$_4$. There are $12!/(1! 1! 2! 2! 1! 3! 1! 1! 4!) = 4,989,600$ permutations of this type.

# 14.4.1A

From the solution to Exercise 13.2.2A we see that the cycle index of the group of permutations of the 25 squares of a $5 \times 5$ chessboard corresponding to the symmetries of a square is $\frac{1}{8} (x_1^{25} + 2 x_1 x_4^6 + x_1 x_2^{12} + 4 x_1^5 x_2^{10})$. Hence, by Pólya's theorem, the pattern inventory when the squares are colored using **black** and *white* is

```
$$\frac{1}{8}((b+w)^{25} + 2(b+w)(b^4+w^4)^6 + (b+w)(b^2+w^2)^{12} + 4(b+w)^5(b^2+w^2)^{10}).$$
```

We seek the coefficient of $b^{15}w^{10}$. We take the terms one by one. The coefficient of $b^{15}w^{10}$ in $(b+w)^{25}$ is C(25,15) = 3,268,760. There is no term involving $b^{15}w^{10}$ in $(b+w)(b^4+w^4)^6$. The term involving $b^{15}w^{10}$ in $(b+w)(b^2+w^2)^{12}$ comes from multiplying $b$ from the first