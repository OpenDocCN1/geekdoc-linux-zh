
STRSV, DTRSV, CTRSV, ZTRSV, STPSV, DTPSV, CTPSV, and ZTPSV

![](img/5b0f44f3be6048723819b26aed7f6f03_561_0.png)

**Output:**
X = (1.0, 2.0, 3.0, 4.0)

### Example 2

This example shows the solution $x \leftarrow A^{-T}x$. Matrix $A$ is a real 4 by 4 upper nonunit triangular matrix, stored in upper-triangular storage mode. Vector $x$ is a vector of length 4.

**Call Statement and Input:**

```
            UPLO TRANSI DIAG N A LDA X INCX
                  'U' , 'T' , 'N' , 4 , A , 4 , X , 1
CALL STRSV( )
```

![](img/5b0f44f3be6048723819b26aed7f6f03_561_1.png)

**Output:**
X = (5.0, 4.0, 3.0, 2.0)

### Example 3

This example shows the solution $x \leftarrow A^{-H}x$. Matrix $A$ is a complex 4 by 4 upper unit triangular matrix, stored in upper-triangular storage mode. Vector $x$ is a vector of length 4.

Note: Because matrix $A$ is unit triangular, the diagonal elements are not referenced. ESSL assumes a value of (1.0, 0.0) for the diagonal elements.

**Call Statement and Input:**

```
            UPLO TRANSI DIAG N A LDA X INCX
                  'U' , 'C' , 'U' , 4 , A , 4 , X , 1
CALL CTRSV( )
```

![](img/5b0f44f3be6048723819b26aed7f6f03_561_2.png)

**Output:**
X = ((5.0, 5.0), (4.0, 4.0), (3.0, 3.0), (2.0, 2.0))

### Example 4

This example shows the solution $x \leftarrow A^{-1}x$. Matrix $A$ is a real 4 by 4 lower unit triangular matrix, stored in lower-triangular-packed storage mode. Vector $x$ is a vector of length 4. Matrix $A$ is:

![](img/5b0f44f3be6048723819b26aed7f6f03_562_0.png)

Note: Because matrix A is unit triangular, the diagonal elements are not referenced. ESSSL assumes a value of 1.0 for the diagonal elements.

Call Statement and Input:

![](img/5b0f44f3be6048723819b26aed7f6f03_562_1.png)

Output:

![](img/5b0f44f3be6048723819b26aed7f6f03_562_2.png)

### Example 5

This example shows the solution $x=A^{-T}x$. Matrix A is a real 4 by 4 upper nonunit triangular matrix, stored in upper-triangular-packed storage mode. Vector x is a vector of length 4. Matrix A is:

![](img/5b0f44f3be6048723819b26aed7f6f03_562_3.png)

Call Statement and Input:

![](img/5b0f44f3be6048723819b26aed7f6f03_562_4.png)

Output:

![](img/5b0f44f3be6048723819b26aed7f6f03_562_5.png)

### Example 6

This example shows the solution $x=A^{-H}x$. Matrix A is a complex 4 by 4 upper unit triangular matrix, stored in upper-triangular-packed storage mode. Vector x is a vector of length 4. Matrix A is:

![](img/5b0f44f3be6048723819b26aed7f6f03_562_6.png)

Note: Because matrix A is unit triangular, the diagonal elements are not referenced. ESSSL assumes a value of (1.0, 0.0) for the diagonal elements.

Call Statement and Input:

```
UPLO TRANSI DIAG N AP X INCX
CALL CTPSV( 'U', 'C', 'U', 4, AP, X, 1 )
```

```
AP = ( , , (2.0, 2.0), , , (3.0, 3.0), (2.0, 2.0), , , (2.0, 2.0), (5.0, 5.0), (3.0, 3.0), , )
```

```
X = ((5.0, 5.0), (24.0, 4.0), (49.0, 3.0), (80.0, 2.0))
```

**Output:**

```
X = ((5.0, 5.0), (4.0, 4.0), (3.0, 3.0), (2.0, 2.0))
```

## STRSM, DTRSM, CTRSM, and ZTRSM—Solution of Triangular Systems of Equations with Multiple Right-Hand Sides

STRSM and DTRSM perform one of the following solves for a triangular system of equations with multiple right-hand sides, using scalar $\alpha$, rectangular matrix $B$, and triangular matrix $A$ or its transpose:

| **Solution** | **Equation** |
|:---|:---|
| 1. $B \leftarrow \alpha (A^{-1})B$ | $AX = \alpha B$ |
| 2. $B \leftarrow \alpha (A^{T})B$ | $A^{T}X = \alpha B$ |
| 3. $B \leftarrow \alpha B(A^{-1})$ | $XA = \alpha B$ |
| 4. $B \leftarrow \alpha B(A^{-T})$ | $XA^{T} = \alpha B$ |

CTRSM and ZTRSM perform one of the following solves for a triangular system of equations with multiple right-hand sides, using scalar $\alpha$, rectangular matrix $B$, and triangular matrix $A$, its transpose, or its conjugate transpose:

| **Solution** | **Equation** |
|:---|:---|
| 1. $B \leftarrow \alpha (A^{-1})B$ | $AX = \alpha B$ |
| 2. $B \leftarrow \alpha (A^{*})B$ | $A^{*}X = \alpha B$ |
| 3. $B \leftarrow \alpha B(A^{-1})$ | $XA = \alpha B$ |
| 4. $B \leftarrow \alpha B(A^{-*})$ | $XA^{*} = \alpha B$ |
| 5. $B \leftarrow \alpha (A^{*})B$ | $A^{*}X = \alpha B$ |
| 6. $B \leftarrow \alpha B(A^{-*})$ | $XA^{*} = \alpha B$ |

**Note:** The term $X$ used in the systems of equations listed above represents the output solution matrix. It is important to note that in these subroutines the solution matrix is actually returned in the input-output argument $b$.

**Table 110. Data Types**

| A, B, $\alpha$ | Subroutine |
|:---|:---|
| Short-precision real | STRSM |
| Long-precision real | DTRSM |
| Short-precision complex | CTRSM |
| Long-precision complex | ZTRSM |

### Syntax

| Language | Syntax |
|:---|:---|
| Fortran | `CALL STRSM \| DTRSM \| CTRSM \| ZTRSM (side, uplo, transa, diag, m, n, alpha, a, lda, b, ldb)` |
| C and C++ | `strsm \| dtrsm \| ctrsm \| ztrsm (side, uplo, transa, diag, m, n, alpha, a, lda, b, ldb);` |

- **On Entry:**
- `side` indicates whether the triangular matrix $A$ is located to the left or right of rectangular matrix $B$ in the system of equations, where:
    - If `side` = 'L', $A$ is to the left of $B$, resulting in solution 1, 2, or 5.
    - If `side` = 'R', $A$ is to the right of $B$, resulting in solution 3, 4, or 6.
    - Specified as: a single character. It must be 'L' or 'R'.

- `uplo` indicates whether matrix $A$ is an upper or lower triangular matrix, where:
    - If `uplo` = 'U', $A$ is an upper triangular matrix.
    - If `uplo` = 'L', $A$ is a lower triangular matrix.
    - Specified as: a single character. It must be 'U' or 'L'.

- `transa` indicates the form of matrix $A$ used in the system of equations, where:
    - If `transa` = 'N', $A$ is used, resulting in solution 1 or 3.
    - If `transa` = 'T', $A^{T}$ is used, resulting in solution 2 or 4.
    - If `transa` = 'C', $A^{H}$ is used, resulting in solution 5 or 6.
    - Specified as: a single character. It must be 'N', 'T', or 'C'.

- `diag` indicates the characteristics of the diagonal of matrix $A$, where:
    - If `diag` = 'U', $A$ is a unit triangular matrix.
    - If `diag` = 'N', $A$ is not a unit triangular matrix.
    - Specified as: a single character. It must be 'U' or 'N'.

- `m` is the number of rows in rectangular matrix $B$, and:
    - If `side` = 'L', $m$ is the order of triangular matrix $A$.
    - Specified as: a fullword integer, where:
        - If `side` = 'L', $0 \le m \le lda$ and $m \le ldb$.
        - If `side` = 'R', $0 \le m \le ldb$.

- `n` is the number of columns in rectangular matrix $B$, and:
    - If `side` = 'R', $n$ is the order of triangular matrix $A$.
    - Specified as: a fullword integer; $n \ge 0$, and:
        - If `side` = 'R', $n \le lda$.

- `alpha` is the scalar $\alpha$. Specified as: a number of the data type indicated in Table 110 on page 541.

- `a` is the triangular matrix $A$, of which only the upper or lower triangular portion is used, where:
    - If `side` = 'L', $A$ is order $m$.
    - If `side` = 'R', $A$ is order $n$.
    - Specified as: a two-dimensional array, containing numbers of the data type indicated in Table 110 on page 541, where:
        - If `side` = 'L', its size must be $lda$ by (at least) $m$.
        - If `side` = 'R', its size must be $lda$ by (at least) $n$.

- `lda` is the leading dimension of the array specified for `a`.
    - Specified as: a fullword integer; $lda > 0$, and:
        - If `side` = 'L', $lda \ge m$.
        - If `side` = 'R', $lda \ge n$.

- `b` is the $m$ by $n$ rectangular matrix $B$, which contains the right-hand sides of the triangular system to be solved.
    - Specified as: an $ldb$ by (at least) $n$ array, containing numbers of the data type indicated in Table 110 on page 541.

- `ldb` is the leading dimension of the array specified for `b`.
    - Specified as: a fullword integer; $ldb > 0$ and $ldb \ge m$.

- **On Return:**
- `b` is the $m$ by $n$ matrix $B$, containing the results of the computation.
    - Returned as: an $ldb$ by (at least) $n$ array, containing numbers of the data type indicated in Table 110 on page 541.

### Notes

1. These subroutines accept lowercase letters for the `transa`, `side`, `diag`, and `uplo` arguments.
2. For STRSM and DTRSM, if you specify 'C' for the `transa` argument, it is interpreted as though you specified 'T'.
3. Matrices $A$ and $B$ must have no common elements or results are unpredictable.
4. If matrix $A$ is upper triangular (`uplo` = 'U'), these subroutines refer to only the upper triangular portion of the matrix. If matrix $A$ is lower triangular, (`uplo` = 'L'), these subroutines refer to only the lower triangular portion of the matrix. The unreferenced elements are assumed to be zero.
5. The elements of the diagonal of a unit triangular matrix are always one, so you do not need to set these values. The ESSL subroutines always assume that the values in these positions are 1.0 for STRSM and DTRSM and (1.0, 0.0) for CTRSM and ZTRSM.
6. For a description of triangular matrices and how they are stored, see "Triangular Matrix" on page 72.

### Function

These subroutines solve a triangular system of equations with multiple right-hand sides. The solution $B$ may be any of the following, where $A$ is a triangular matrix and $B$ is a rectangular matrix:

1. $B \leftarrow \alpha (A^{-1})B$
2. $B \leftarrow \alpha (A^{-T})B$
3. $B \leftarrow \alpha B (A^{-1})$
4. $B \leftarrow \alpha B (A^{-T})$
5. $B \leftarrow \alpha (A^{-H})B$ (only for CTRSM and ZTRSM)
6. $B \leftarrow \alpha B (A^{-H})$ (only for CTRSM and ZTRSM)

where:

- $\alpha$ is a scalar.
- $B$ is an $m$ by $n$ rectangular matrix.
- $A$ is an upper or lower triangular matrix, where:
    - If `side` = 'L', it has order $m$, and equation 1, 2, or 5 is performed.
    - If `side` = 'R', it has order $n$, and equation 3, 4, or 6 is performed.

If $n$ or $m$ is 0, no computation is performed. See references [34] and [38].

### Error Conditions

- **Resource Errors:** Unable to allocate internal work area.
- **Computational Errors:** None
- **Input-Argument Errors:**

Note: If the triangular matrix $A$ is singular, the results returned by this subroutine are unpredictable, and there may be a divide-by-zero program exception message.
