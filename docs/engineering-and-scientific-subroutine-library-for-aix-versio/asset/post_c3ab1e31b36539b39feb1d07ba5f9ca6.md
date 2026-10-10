
## SGEMM, DGEMM, CGEMM, and ZGEMM

![](img/5b0f44f3be6048723819b26aed7f6f03_419_0.png)

### Example 2

This example shows the computation $C \leftarrow \alpha A B^{T} + \beta C$, where A and C are contained in larger arrays A and C, respectively, and B is the same size as array B in which it is contained.

Call Statement and Input:

```
TRANSA TRANSB L N M ALPHA A LDA B LDB BETA C LDC
CALL SGEMM( 'N', 'T', 3, 3, 2, 1.0, A, 4, B, 3, 2.0, C, 5 )
```

![](img/5b0f44f3be6048723819b26aed7f6f03_419_1.png)

![](img/5b0f44f3be6048723819b26aed7f6f03_419_2.png)

Output:

![](img/5b0f44f3be6048723819b26aed7f6f03_419_3.png)

### Example 3

This example shows the computation $C \leftarrow \alpha A B + \beta C$ using complex data, where A, B, and C are contained in larger arrays, A, B, and C, respectively.

Call Statement and Input:

```
TRANSA TRANSB L N M ALPHA A LDA B LDB BETA C LDC
CALL CGEMM( 'N', 'N', 6, 2, 3, ALPHA, A, 8, B, 4, BETA, C, 8 )
ALPHA = (1.0, 0.0)
BETA = (2.0, 0.0)
```

![](img/5b0f44f3be6048723819b26aed7f6f03_419_4.png)

$$\begin{matrix} & & [ \ldots & \ldots & \ldots ] \\ B = & & \begin{matrix} (1.0, \ 8.0) & (2.0, \ 7.0) \\ (4.0, \ 4.0) & (6.0, \ 8.0) \\ (6.0, \ 2.0) & (4.0, \ 5.0) \end{matrix} \\ & & \ldots & & \ldots \end{matrix}$$

$$\begin{matrix} & & \begin{matrix} (0.5, \ 0.0) & (0.5, \ 0.0) \\ (0.5, \ 0.0) & (0.5, \ 0.0) \\ (0.5, \ 0.0) & (0.5, \ 0.0) \end{matrix} \\ C = & & \begin{matrix} (0.5, \ 0.0) & (0.5, \ 0.0) \\ (0.5, \ 0.0) & (0.5, \ 0.0) \\ (0.5, \ 0.0) & (0.5, \ 0.0) \end{matrix} \\ & & \ldots & & \ldots \end{matrix}$$

Output:

$$\begin{matrix} & & \begin{matrix} (-22.0, \ 113.0) & (-35.0, \ 142.0) \\ (-19.0, \ 114.0) & (-35.0, \ 141.0) \end{matrix} \\ C = & & \begin{matrix} (-20.0, \ 119.0) & (-43.0, \ 146.0) \\ (-27.0, \ 110.0) & (-58.0, \ 131.0) \end{matrix} \\ & & \begin{matrix} (8.0, \ 103.0) & (0.0, \ 112.0) \\ (-55.0, \ 116.0) & (-75.0, \ 135.0) \end{matrix} \\ & & \ldots & & \ldots \end{matrix}$$

### Example 4

This example shows how to obtain the conjugate transpose of $AB^{H}$.

$$(AB^{H})^{H} = \overline{BA}^{T} = BA^{H}$$

This shows the conjugate transpose of the computation performed in “Example 8” on page 385 for CGEMUL, which uses the following calling sequence:

`CALL CGEMUL(A, 4, 'N', B, 3, 'C', C, 4, 3, 2, 3)`

You instead code the calling sequence for $C=\beta C+\alpha BA^{H}$, where $\beta = 0$, $\alpha = 1$, and the array $C$ has the correct dimensions to receive the transposed matrix. Because $\beta$ is zero, $\beta C = 0$. For a description of all the matrix identities, see “Special Usage” on page 380.

Call Statement and Input:

$$\begin{matrix} TRANS A & TRANS B & L & N & M & ALPHA & A & LDA & B & LDB & BETA & C & LDC \\ CALL \ CGEMN( & ‘N’, & ‘C’, & 3, & 3, & 2, & ALPHA, & B, & 3, & A, & 3, & BETA, & C, & 4 ) \\ ALPHA = & (1.0, \ 0.0) \\ BETA = & (0.0, \ 0.0) \end{matrix}$$

$$\begin{matrix} & & \begin{matrix} (1.0, \ 3.0) & (-3.0, \ 2.0) \\ (2.0, \ 5.0) & (4.0, \ 6.0) \end{matrix} \\ B = & & \begin{matrix} (1.0, \ 1.0) & (-1.0, \ 9.0) \end{matrix} \end{matrix}$$

A = [ (1.0, 2.0) (-3.0, 2.0) ]
[ (2.0, 6.0) (4.0, 5.0) ]
[ (1.0, 2.0) (-1.0, 8.0) ]

C = (not relevant)

Output:

C = [ (20.0, 1.0) (18.0, 23.0) (26.0, 23.0) ]
[ (12.0, -25.0) (80.0, 2.0) (56.0, -37.0) ]
[ (24.0, -26.0) (49.0, 37.0) (76.0, -2.0) ]

### Example 5

This example shows the computation $C\leftarrow\alpha A^{H}B^{H}+\beta C$ using complex data, where $A$, $B$, and $C$ are the same size as the arrays $A$, $B$, and $C$, in which they are contained. Because $\beta$ is zero, $\beta C = 0$. (Based on the dimensions of the matrices, $A$ is actually a column vector, and $C$ is actually a row vector.)

Call Statement and Input:

```
TRANS$A$ TRANS$B$ L N M ALPHA A LDA B LDB BETA C LDC
CALL CGEMM( 'T' , 'C' , 1 , 3 , 3 , ALPHA , A , 3 , B , 3 , BETA , C , 1 )
ALPHA = (1.0, 1.0)
BETA = (0.0, 0.0)

A = [ (1.0, 2.0) ]
    [ (2.0, 5.0) ]
    [ (1.0, 6.0) ]

B = [ (1.0, 6.0) (-3.0, 4.0) (2.0, 6.0) ]
    [ (2.0, 3.0) (4.0, 6.0) (0.0, 3.0) ]
    [ (1.0, 3.0) (-1.0, 6.0) (-1.0, 9.0) ]

C = (not relevant)

Output:
C = [ (86.0, 44.0) (58.0, 70.0) (121.0, 55.0) ]
```

## SSYMM, DSYMM, CSYMM, ZSYMM, CHEMM, and ZHEMM—Matrix-Product Where One Matrix is Real or Complex Symmetric or Complex Hermitian

These subroutines compute one of the following matrix-matrix products, using the scalars $\alpha$ and $\beta$ and matrices $A$, $B$, and $C$:

1. $C \leftarrow \alpha AB + \beta C$
2. $C \leftarrow \alpha BA + \beta C$

where matrix $A$ is stored in either upper or lower storage mode, and:

- For SSYMM and DSYMM, matrix $A$ is real symmetric.
- For CSYMM and ZSYMM, matrix $A$ is complex symmetric.
- For CHEMM and ZHEMM, matrix $A$ is complex Hermitian.

### Table 81. Data Types

| $\alpha, B, \beta, C$ | Subprogram |
| :--- | :--- |
| Short-precision real | SSYMM |
| Long-precision real | DSYMM |
| Short-precision complex | CSYMM and CHEMM |
| Long-precision complex | ZSYMM and ZHEMM |

### Syntax

| | |
| :--- | :--- |
| Fortran | `CALL SSYMM \| DSYMM \| CSYMM \| ZSYMM \| CHEMM \| ZHEMM (side, uplo, m, n, alpha, a, lda, b, ldb, beta, c, ldc)` |
| C and C++ | `ssymm \| dsymm \| csymm \| zsymm \| chemm \| zhemm (side, uplo, m, n, alpha, a, lda, b, ldb, beta, c, ldc);` |

On Entry:

*side* indicates whether matrix $A$ is located to the left or right of rectangular matrix $B$ in the equation used for this computation, where:

If $side =$ 'L', $A$ is to the left of $B$, resulting in equation 1.  
If $side =$ 'R', $A$ is to the right of $B$, resulting in equation 2.  
Specified as: a single character. It must be 'L' or 'R'.

*uplo* indicates the storage mode used for matrix $A$, where:

If $uplo =$ 'U', $A$ is stored in upper storage mode.  
If $uplo =$ 'L', $A$ is stored in lower storage mode.  
Specified as: a single character. It must be 'U' or 'L'.

$m$ is the number of rows in rectangular matrices $B$ and $C$, and:

If $side =$ 'L', $m$ is the order of matrix $A$.  
Specified as: a fullword integer; $0 \le m \le lb$, $m \le ld_c$, and:  
If $side =$ 'L', $m \le ld_a$.

$n$ is the number of columns in rectangular matrices $B$ and $C$, and:

If $side =$ 'R', $n$ is the order of matrix $A$.  
Specified as: a fullword integer; $n \ge 0$ and:

If *side* = '`R`', $n \leq lda$.

*alpha* is the scalar $\alpha$.

Specified as: a number of the data type indicated in Table 81 on page 399.

*a* is the real symmetric, complex symmetric, or complex Hermitian matrix $A$, where:
If *side* = '`L`', $A$ is order $m$.
If *side* = '`R`', $A$ is order $n$.
and where it is stored as follows:
If *uplo* = '`U`', $A$ is stored in upper storage mode.
If *uplo* = '`L`', $A$ is stored in lower storage mode.

Specified as: a two-dimensional array, containing numbers of the data type indicated in Table 81 on page 399, where:
If *side* = '`L`', its size must be $lda$ by (at least) $m$.
If *side* = '`R`', its size must be $lda$ by (at least) $n$.

*lda* is the leading dimension of the array specified for *a*.
Specified as: a fullword integer; $lda > 0$ and:
If *side* = '`L`', $lda \geq m$.
If *side* = '`R`', $lda \geq n$.

*b* is the $m$ by $n$ rectangular matrix $B$.
Specified as: an $ldb$ by (at least) $n$ array, containing numbers of the data type indicated in Table 81 on page 399.

*ldb* is the leading dimension of the array specified for *b*.
Specified as: a fullword integer; $ldb > 0$ and $ldb \geq m$.

*beta* is the scalar $\beta$.
Specified as: a number of the data type indicated in Table 81 on page 399.

*c* is the $m$ by $n$ rectangular matrix $C$.
Specified as: an $ldc$ by (at least) $n$ array, containing numbers of the data type indicated in Table 81 on page 399.

*ldc* is the leading dimension of the array specified for *c*.
Specified as: a fullword integer; $ldc > 0$ and $ldc \geq m$.

### On Return:

*c* is the $m$ by $n$ matrix $C$, containing the results of the computation.
Returned as: an $ldc$ by (at least) $n$ array, containing numbers of the data type indicated in Table 81 on page 399.

### Notes

1. These subroutines accept lowercase letters for the *side* and *uplo* arguments.
2. Matrices $A$, $B$, and $C$ must have no common elements; otherwise, results are unpredictable.
3. If matrix $A$ is upper triangular (*uplo* = '`U`'), these subroutines use only the data in the upper triangular portion of the array. If matrix $A$ is lower triangular,
