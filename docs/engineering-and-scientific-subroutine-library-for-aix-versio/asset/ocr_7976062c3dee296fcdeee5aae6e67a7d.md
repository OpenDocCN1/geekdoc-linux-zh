# SGEMV, DGEMV, CGEMV, ZGEMV, SGEMX, DGEMX, SGEMTX, and DGEMTX

A = (same as input A in Example 1)
X = (3.0, 2.0, 1.0, 4.0)
Y = (1.0, ., 2.0, ., 3.0)

Output:
Y = (28.0, ., 24.0, ., 29.0)

# Example 3

This example shows the computation for TRANSa equal to 'N', where the complex general matrix A is used in the computation.

**Call Statement and Input:**

```
TRANSa M N ALPHA A LDA X INCX BETA Y INCY
| | | | | | | | | | | |
CALL CGEMV('N', 5, 3, ALPHA, A, 10, X, 1, BETA, Y, 1)

ALPHA = (1.0, 0.0)
```

A = [
(1.0, 2.0) (3.0, 5.0) (2.0, 0.0)
(2.0, 3.0) (7.0, 9.0) (4.0, 8.0)
(7.0, 4.0) (1.0, 4.0) (6.0, 0.0)
(8.0, 2.0) (2.0, 5.0) (8.0, 0.0)
(9.0, 1.0) (3.0, 6.0) (1.0, 0.0)
. . .
. . .
. . .
. . .
. . .
]

X = ((1.0, 2.0), (4.0, 0.0), (1.0, 1.0))
BETA = (1.0, 0.0)
Y = ((1.0, 2.0), (4.0, 0.0), (1.0, -1.0), (3.0, 4.0),
(2.0, 0.0))

Output:
Y = ((12.0, 28.0), (24.0, 55.0), (10.0, 39.0), (23.0, 50.0),
(22.0, 44.0))

# Example 4

This example shows the computation for TRANSa equal to 'T', where the transpose of complex general matrix A is used in the computation. Because β is zero, the result of the computation is $\alpha A^{T}x$.

**Call Statement and Input:**

```
TRANSa M N ALPHA A LDA X INCX BETA Y INCY
| | | | | | | | | | | |
CALL CGEMV('T', 5, 3, ALPHA, A, 10, X, 1, BETA, Y, 1)

ALPHA = (1.0, 0.0)
A = (same as input A in Example 3)
X = ((1.0, 2.0), (4.0, 0.0), (1.0, 1.0), (3.0, 4.0),
(2.0, 0.0))
BETA = (0.0, 0.0)
Y = (not relevant)
```

Output:
Y = ((42.0, 67.0), (10.0, 87.0), (50.0, 74.0))