# STBSV, DTBSV, CTBSV, and ZTBSV

Output:

X = (1.0, 1.0, 0.0, 1.0, 0.0, 2.0, 0.0, 1.0, 3.0)

# Example 2

This example shows the solution $x = A^{-T}x$, solving the same system as in Example 1. Matrix A is a real 9 by 9 lower triangular band matrix with a lower band width of 2 that is not unit triangular, stored in lower-triangular-band-packed storage mode. Vector x is a vector of length 9 where matrix A is:

1.0 0.0 0.0 0.0 0.0 0.0 0.0 0.0 0.0
1.0 4.0 0.0 0.0 0.0 0.0 0.0 0.0 0.0
1.0 2.0 4.0 0.0 0.0 0.0 0.0 0.0 0.0
0.0 3.0 1.0 4.0 0.0 0.0 0.0 0.0 0.0
0.0 0.0 1.0 2.0 3.0 0.0 0.0 0.0 0.0
0.0 0.0 0.0 2.0 1.0 3.0 0.0 0.0 0.0
0.0 0.0 0.0 0.0 1.0 2.0 3.0 0.0 0.0
0.0 0.0 0.0 0.0 0.0 2.0 1.0 2.0 0.0
0.0 0.0 0.0 0.0 0.0 0.0 0.0 2.0 1.0

Call Statement and Input:

```
UPLO TRANS DIAG N K A LDA X INCX
|
| |
CALL STBSV( 'L', 'T', 'N', , 9, 2, A, 3, X, 1 )
```

1.0 4.0 4.0 4.0 3.0 3.0 3.0 2.0 1.0
1.0 2.0 1.0 2.0 1.0 2.0 1.0 2.0 .
1.0 3.0 1.0 2.0 1.0 2.0 0.0 . .

X = (same as input X in Example 1)

Output:

X = (same as output X in Example 1)

# Example 3

This example shows the solution $x = A^{-T}x$, where $k > n$. Matrix A is a real 4 by 4 upper triangular band matrix with an upper band width of 3, even though k is specified as 5. It is not unit triangular and is stored in upper-triangular-band-packed storage mode. Vector x is a vector of length 4 where matrix A is:

1.0 2.0 3.0 2.0
0.0 2.0 2.0 5.0
0.0 0.0 3.0 3.0
0.0 0.0 0.0 1.0

Call Statement and Input:

```
UPLO TRANS DIAG N K A LDA X INCX
|
| |
CALL STBSV( 'U', 'T', 'N', , 4, 5, A, 6, X, 1 )
```

. . . .
. . . .
. . . 2.0
. 3.0 5.0
. 2.0 2.0 3.0