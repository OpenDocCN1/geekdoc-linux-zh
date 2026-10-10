
# SSYRK, DSYRK, CSYRK, ZSYRK, CHERK, and ZHERK

![](img/5b0f44f3be6048723819b26aed7f6f03_439_0.png)

![](img/5b0f44f3be6048723819b26aed7f6f03_439_1.png)

Output:

![](img/5b0f44f3be6048723819b26aed7f6f03_439_2.png)

## Example 3

This example shows the computation $C \leftarrow \alpha A^T + \beta C$, where A is a 3 by 5 complex rectangular matrix, and C is a complex symmetric matrix of order 3, stored in upper storage mode.

**Call Statement and Input:**

```fortran
  UPLO TRANS     N    K    ALPHA     A     LDA     BETA     C     LDC
CALL CSYRK ('U', 'N', 3, 5, ALPHA, A, 3, BETA, C, 4 )
ALPHA  = (1.0, 1.0)
BETA   = (1.0, 1.0)
```

![](img/5b0f44f3be6048723819b26aed7f6f03_439_3.png)

![](img/5b0f44f3be6048723819b26aed7f6f03_439_4.png)

Output:

![](img/5b0f44f3be6048723819b26aed7f6f03_439_5.png)

## Example 4

This example shows the computation $C \leftarrow \alpha A^H + \beta C$, where A is a 5 by 3 complex rectangular matrix, and C is a complex Hermitian matrix of order 3, stored in lower storage mode.

**Note:** The imaginary parts of the diagonal elements of a complex Hermitian matrix are assumed to be zero, so you do not have to set these values. On output, they are set to zero.

**Call Statement and Input:**

```fortran
       UPLO TRANS      N   K   ALPHA     A   LDA  BETA     C   LDC
         |    |          |   |    |       |   |    |       |   |
CALL CHERK( 'L' , 'C' ,   3 ,  5 ,   1.0 ,  A ,  5 ,  1.0 ,  C ,  4 )
```

```fortran
A = [(2.0, 0.0) (3.0, 2.0) (4.0, 1.0)  
     (3.0, 3.0) (8.0, 0.0) (2.0, 5.0)  
     (1.0, 3.0) (2.0, 1.0) (6.0, 0.0)  
     (3.0, 3.0) (8.0, 0.0) (2.0, 5.0)  
     (1.0, 9.0) (3.0, 0.0) (6.0, 7.0)]
```

```fortran
C = [(6.0, . ) . . 
     (3.0, 4.0) (10.0, . ) . 
     (9.0, 1.0) (12.0, 2.0) (3.0, . ) 
     . . .]
```

**Output:**

```fortran
C = [(138.0, 0.0) . . 
     (65.0, 80.0) (165.0, 0.0) . 
     (134.0, 46.0) (88.0, -88.0) (199.0, 0.0) 
     . . .]
```

# SSYR2K, DSYR2K, CSYR2K, ZSYR2K, CHER2K, and ZHER2K—Rank-2K Update of a Real or Complex Symmetric or a Complex Hermitian Matrix

These subroutines compute one of the following rank-2k updates, where matrix C is stored in upper or lower storage mode. SSYR2K, DSYR2K, CSYR2K, and ZSYR2K use the scalars $\alpha$ and $\beta$, real or complex matrices A and B or their transposes, and real or complex symmetric matrix C to compute:

1. $C \leftarrow \alpha AB^{\mathrm{T}} + \alpha BA^{\mathrm{T}} + \beta C$
2. $C \leftarrow \alpha A^{\mathrm{T}} B + \alpha B^{\mathrm{T}} A + \beta C$

CHER2K and ZHER2K use the scalars $\alpha$ and $\beta$, complex matrices A and B or their complex conjugate transposes, and complex Hermitian matrix C to compute:

3. $C \leftarrow \alpha AB^{\mathrm{H}} + \overline{\alpha} BA^{\mathrm{H}} + \beta C$
4. $C \leftarrow \alpha A^{\mathrm{H}} B + \overline{\alpha} B^{\mathrm{H}} A + \beta C$

### Table 84. Data Types

| A, B, C, $\alpha$ | $\beta$ | Subprogram |
| :---------------- | :---------------- | :---------------- |
| Short-precision real | Short-precision real | SSYR2K |
| Long-precision real | Long-precision real | DSYR2K |
| Short-precision complex | Short-precision complex | CSYR2K |
| Long-precision complex | Long-precision complex | ZSYR2K |
| Short-precision complex | Short-precision real | CHER2K |
| Long-precision complex | Long-precision real | ZHER2K |

### Syntax

| Fortran | CALL SSYR2K \| DSYR2K \| CSYR2K \| ZSYR2K \| CHER2K \| ZHER2K (uplo, trans, n, k, alpha, a, lda, b, ldb, beta, c, ldc) |
| :------ | :--------------------------------------------------------------------------------------------------------------------------------- |
| C and C++ | ssyr2k \| dsyr2k \| csyr2k \| zssyr2k \| cher2k \| zher2k (uplo, trans, n, k, alpha, a, lda, b, ldb, beta, c, ldc); |

### On Entry:

- **uplo**
    - indicates the storage mode used for matrix C, where:
        - If uplo = 'U', C is stored in upper storage mode.
        - If uplo = 'L', C is stored in lower storage mode.
        - Specified as: a single character. It must be 'U' or 'L'.
- **trans**
    - indicates the form of matrices A and B to use in the computation, where:
        - If trans = 'N', A and B are used, resulting in equation 1 or 3.
        - If trans = 'T', $A^{T}$ and $B^{T}$ are used, resulting in equation 2.
        - If trans = 'C', $A^{H}$ and $B^{H}$ are used, resulting in equation 4.
        - Specified as: a single character, where:
            - For SSYR2K and DSYR2K, it must be 'N', 'T', or 'C'.
            - For CSYR2K and ZSYR2K, it must be 'N' or 'T'.
            - For CHER2K and ZHER2K, it must be 'N' or 'C'.
- **n** is the order of matrix *C*.
    - Specified as: a fullword integer; $0 \leq n \leq$ *ldc* and:
        - If *trans* = 'N', then $n \leq$ *lda* and $n \leq$ *ldb*.
- **k** has the following meaning, where:
    - If *trans* = 'N', it is the number of columns in matrices *A* and *B*.
    - If *trans* = 'T' or 'C', it is the number of rows in matrices *A* and *B*.
    - Specified as: a fullword integer; $k \geq 0$ and:
        - If *trans* = 'T' or 'C', then $k \leq$ *lda* and $k \leq$ *ldb*.
- **alpha** is the scalar $\alpha$.
    - Specified as: a number of the data type indicated in Table 84.
- **a** is the rectangular matrix *A*, where:
    - If *trans* = 'N', *A* is *n* by *k*.
    - If *trans* = 'T' or 'C', *A* is *k* by *n*.
    - **Note:** No data should be moved to form $A^{T}$ or $A^{H}$; that is, the matrix *A* should always be stored in its untransposed form.
    - Specified as: a two-dimensional array, containing numbers of the data type indicated in Table 84, where:
        - If *trans* = 'N', its size must be *lda* by (at least) *k*.
        - If *trans* = 'T' or 'C', its size must be *lda* by (at least) *n*.
- **lda** is the leading dimension of the array specified for *a*.
    - Specified as: a fullword integer; *lda* $> 0$ and:
        - If *trans* = 'N', *lda* $\geq n$.
        - If *trans* = 'T' or 'C', *lda* $\geq k$.
- **b** is the rectangular matrix *B*, where:
    - If *trans* = 'N', *B* is *n* by *k*.
    - If *trans* = 'T' or 'C', *B* is *k* by *n*.
    - **Note:** No data should be moved to form $B^{T}$ or $B^{H}$; that is, the matrix *B* should always be stored in its untransposed form.
    - Specified as: a two-dimensional array, containing numbers of the data type indicated in Table 84, where:
        - If *trans* = 'N', its size must be *ldb* by (at least) *k*.
        - If *trans* = 'T' or 'C', its size must be *ldb* by (at least) *n*.
- **ldb** is the leading dimension of the array specified for *b*.
    - Specified as: a fullword integer; *ldb* $> 0$ and:
        - If *trans* = 'N', *ldb* $\geq n$.
        - If *trans* = 'T' or 'C', *ldb* $\geq k$.
- **beta** is the scalar $\beta$.
    - Specified as: a number of the data type indicated in Table 84.
- **c** is matrix **C** of order *n*, which is real symmetric, complex symmetric, or complex Hermitian, where:
    - If *uplo* = 'U', **C** is stored in upper storage mode.
    - If *uplo* = 'L', **C** is stored in lower storage mode.
    - Specified as: an *ldc* by (at least) *n* array, containing numbers of the data type indicated in Table 84.
- **ldc** is the leading dimension of the array specified for *c*.
    - Specified as: a fullword integer; *ldc* $> 0$ and *ldc* $\geq$ *n*.

### On Return:

- **c** is matrix **C** of order *n*, which is real symmetric, complex symmetric, or complex Hermitian, containing the results of the computation, where:
    - If *uplo* = 'U', **C** is stored in upper storage mode.
    - If *uplo* = 'L', **C** is stored in lower storage mode.
    - Returned as: an *ldc* by (at least) *n* array, containing numbers of the data type indicated in Table 84.

### Notes

1. These subroutines accept lowercase letters for the *uplo* and *trans* arguments.
2. For SSYR2K and DSYR2K, if you specify 'C' for the *trans* argument, it is interpreted as though you specified 'T'.
3. Matrices **A** and **B** must have no common elements with matrix **C**; otherwise, results are unpredictable.
4. The imaginary parts of the diagonal elements of a complex Hermitian matrix **C** are assumed to be zero, so you do not have to set these values. On output, they are set to zero, except when $\beta$ is one and $\alpha$ is one or $\mathbf{k}$ is zero, in which case no computation is performed.
5. For a description of how symmetric matrices are stored in upper and lower storage mode, see “Symmetric Matrix” on page 64. For a description of how complex Hermitian matrices are stored in upper and lower storage mode, see “Complex Hermitian Matrix” on page 69.

### Function

These subroutines can perform the following rank-2k updates. For SSYR2K and DSYR2K, matrix **C** is real symmetric. For CSYR2K and ZSYR2K, matrix **C** is complex symmetric. They perform:

1. $\mathbf{C} \leftarrow \alpha \mathbf{A}\mathbf{B}^t + \alpha \mathbf{B}\mathbf{A}^t + \beta \mathbf{C}$
2. $\mathbf{C} \leftarrow \alpha \mathbf{A}^t\mathbf{B} + \alpha \mathbf{B}^t\mathbf{A} + \beta \mathbf{C}$

For CHER2K and ZHER2K, matrix **C** is complex Hermitian. They perform:
