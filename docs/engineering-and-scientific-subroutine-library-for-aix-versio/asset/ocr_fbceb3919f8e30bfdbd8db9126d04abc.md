# STBMV, DTBMV, CTBMV, and ZTBMV

# Function

These subroutines can perform the following matrix-vector product computations, using the triangular band matrix *A*, its transpose, or its conjugate transpose, where *A* can be either upper or lower triangular:

```
x\*Ax
x\*A^T x
x\*A^H x (for CTBMV and ZTBMV only)
```

where:

+   - *x* is a vector of length *n*.
+   - *A* is an upper or lower triangular band matrix of order *n*, stored in upper- or lower-triangular-band-packed storage mode, respectively.

See references [36], [48], and [40]. If *n* is 0, no computation is performed.

# Error Conditions

Computational Errors: None

+   **Input-Argument Errors:**
+   1. *uplo* \* 'L' or 'U'
+   2. *transa* \* 'T', 'N', or 'C'
+   3. *diag* \* 'N' or 'U'
+   4. *n* < 0
+   5. *k* < 0
+   6. *lda* ≤ 0
+   7. *lda* < *k*+1
+   8. *incx* = 0

# Example 1

This example shows the computation x\*Ax. Matrix *A* is a real 7 by 7 upper triangular band matrix with a half band width of 3 that is not unit triangular, stored in upper-triangular-band-packed storage mode. Vector *x* is a vector of length 7. Matrix *A* is:

```
      [ 1.0  1.0  1.0  1.0  0.0  0.0  0.0
        0.0  2.0  2.0  2.0  2.0  0.0  0.0
        0.0  0.0  3.0  3.0  3.0  3.0  0.0
        0.0  0.0  0.0  4.0  4.0  4.0  4.0
        0.0  0.0  0.0  0.0  5.0  5.0  5.0
        0.0  0.0  0.0  0.0  0.0  6.0  6.0
        0.0  0.0  0.0  0.0  0.0  0.0  7.0
      ]
```

**Call Statement and Input:**

```
          UPLO TRANSA DIAG N   K   LDA X    INCX
          |
          'U'  'N'   'N'  7 , 3 , A , X , 1 )
           |  |

```

```
       A       =          [  .   .   .   1.0  2.0  3.0  4.0
                           .   .   .   1.0  2.0  3.0  4.0  5.0
                           .   .   1.0  2.0  3.0  4.0  5.0  6.0
                           1.0  2.0  3.0  4.0  5.0  6.0  7.0
                           .   .   .   .   .   .   .
       ]
```

```
       X       =          (1.0, 2.0, 3.0, 4.0, 5.0, 6.0, 7.0)
```

**Output:**