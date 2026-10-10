
## SSPSV, DPSV, CHPSV, and ZHPSV

- For $i opt = 1, 11, 21,$ or $31$, the eigenvalues and eigenvectors are computed as follows:
  1. Reduce the real symmetric matrix $\boldsymbol{A}$ (for SPSV and DPSV) or complex Hermitian matrix $\boldsymbol{A}$ (for CHPSV and ZHPSV) to a real symmetric tridiagonal matrix using orthogonal similarity transformations (for SPSV and DPSV) or unitary similarity transforms (for CHPSV and ZHPSV).
  2. Compute the $m$ smallest eigenvalues or $m$ largest eigenvalues of the real symmetric tridiagonal matrix using a rational variant of the QR method with Newton corrections.
  3. Compute the corresponding eigenvectors of the real symmetric tridiagonal matrix using inverse iteration.
  4. Back transform the eigenvectors of the real symmetric tridiagonal matrix to those of the original matrix.
  5. The eigenvalues are returned in vector $\boldsymbol{w}$ in the first $m$ positions, where the $m$ smallest are placed in ascending order, or the $m$ largest are placed in descending order. The corresponding eigenvectors are returned in matrix $\boldsymbol{Z}.$

## Error Conditions

**Resource Errors**: Error 2015 is unrecoverable, $naux = 0$, and unable to allocate work area.

**Computational Errors**:

1. Eigenvale $(i)$ failed to converge after $(xxx)$ iterations. (The computational error message may occur multiple times with processing continuing after each error, because the number of allowable errors for error code 2114 is set to be unlimited in the ESSSL error option table.)
   - The eigenvalue, $w_{j}$, is the best estimate obtained. Any eigenvalues for which this message has not been issued are correct.
   - $ap$ is modified.
   - The return code is set to $1$.
   - $i$ and $xxx$ can be determined at run time by use of the ESSSL error-handling facilities. To obtain this information, you must use ERRSET to change the number of allowable errors for error 2199 in the ESSSL error option table. See "What Can You Do about ESSL Computational Errors?" on page 47.
2. Eigenvector $(i)$ failed to converge after $(xxx)$ iterations. (The computational error message may occur multiple times with processing continuing after each error, because the number of allowable errors for error code 2102 is set to be unlimited in the ESSSL error option table.)
   - All eigenvalues are correct.
   - The eigenvector that failed to converge is set to zero; however, any selected eigenvectors for which this message is not issued are correct.
   - $ap$ is modified.
   - The return code is set to 2.
   - $i$ and $xxx$ can be determined at run time by use of the ESSSL error-handling facilities. To obtain this information, you must use ERRSET to change the number of allowable errors for error 2199 in the ESSSL error option table. See "What Can You Do about ESSL Computational Errors?" on page 47.

**Input-Argument Errors**:

1. $i opt \ne 0$, 1, 10, 11, 20, 21, 30, or 31
2. $n < 0$
3. $m < 0$
4. $m > n$
5. $ldz \le 0$ and $i opt = 1, 11, 21,$ or 31
6. $n > ldz$ and $i opt = 1, 11, 21,$ or 31
7. Error 2015 is recoverable or naux=0, and naux is too small—that is, less than the minimum required value. Return code 3 is returned if error 2015 is recoverable.

## Example 1

This example shows how to find the two smallest eigenvalues and corresponding eigenvectors of a real long-precision symmetric matrix A of order 4, stored in upper-packed storage mode. Matrix A is:

```
5.0 4.0 1.0 1.0
4.0 5.0 1.0 1.0
1.0 1.0 4.0 2.0
1.0 1.0 2.0 4.0
```

where:

- NAUX is equal to 9N.
- AUX contains 9N elements.
- On output, AP has been overwritten.

Note: This matrix is used in Example 4.1 in referenced text [65].

### Call Statement and Input:

```
IOPT AP W Z LDZ N M AUX NAUX
      CALL DSPSV( 21, AP, W, Z, 4, 4, 2, AUX, 36 )
```

```
AP = (5.0, 4.0, 5.0, 1.0, 1.0, 4.0, 1.0, 1.0, 2.0, 4.0)
```

### Output:

```
W = [ 1.000000
      2.000000
      .
      ]
```

```
Z = [ -0.707107   0.000000
      0.707107    0.000000
      0.000000    -0.707107
      0.000000     0.707107 ]
```

## Example 2

This example shows how to find the three largest eigenvalues and corresponding eigenvectors of a real long-precision symmetric matrix A of order 4, stored in lower-packed storage mode, having an eigenvalue of multiplicity two. Matrix A is:

```
6.0 4.0 4.0 1.0
4.0 6.0 1.0 4.0
4.0 1.0 6.0 4.0
1.0 4.0 4.0 6.0
```

where:

- NAUX is equal to 9N.
- AUX contains 9N elements.
- On output, AP has been overwritten.

Note: This matrix is used in Example 4.2 in referenced text [65].

### Call Statement and Input:

```
IOPT   AP    W    Z   LDZ   N     M     AUX    NAUX
CALL DSPSV( 11 , AP , W , Z , 8 , 4 , 3 , AUX , 36 )
```

AP = ( 6.0, 4.0, 4.0, 1.0, 6.0, 1.0, 4.0, 6.0, 4.0, 6.0)

### Output:

W = [ 15.000000
      5.000000
      5.000000
      .
      ]

Z = [ 0.500000  0.707107  0.000000
      0.500000  0.000000 -0.707107
      0.500000  0.000000  0.707107
      0.500000 -0.707107  0.000000
      .        .          .
      .        .          .
      .        .          .
      ]

## Example 3

This example shows how to find the largest eigenvalue and the corresponding eigenvector of a complex Hermitian matrix $A$ of order 2, stored in lower-packed storage mode. Matrix $A$ is:

(1.0, 0.0)  (0.0, -1.0)
(0.0, 1.0)  (1.0, 0.0)

where:

- NAUX is equal to 11N.
- AUX contains 11N elements.
- On output, AP has been overwritten.

Note: This matrix is used in Example 6.1 in referenced text [65].

### Call Statement and Input:

```
IOPT   AP    W    Z   LDZ   N     M     AUX    NAUX
CALL ZHPSV( 11 , AP , W , Z , 2 , 2 , 1 , AUX , 22 )
```

AP = ((1.0, . ), (0.0, 1.0), (1.0, . ))

### Output:

W = [ 2.000000
      .
      ]

Z = [ (0.000000, -0.707107)
      (0.707107,  0.000000)
      ]

## Example 4

This example shows how to find the two smallest eigenvalues only of a complex Hermitian matrix $A$ of order 4, stored in upper-packed storage mode. Matrix $A$ is:

![](img/5b0f44f3be6048723819b26aed7f6f03_753_0.png)

where:

- NAUX is equal to 5N.
- AUX contains 5N elements.
- LDZ is set to 1 to avoid an error condition.
- DUMMY is used as a placeholder for argument z, which is not used in the computation.
- On output, AP has been overwritten.

Note: This matrix is used in Example 6.6 in referenced text [65].

### Call Statement and Input:

![](img/5b0f44f3be6048723819b26aed7f6f03_753_1.png)

![](img/5b0f44f3be6048723819b26aed7f6f03_753_2.png)

### Output:

![](img/5b0f44f3be6048723819b26aed7f6f03_753_3.png)

## SGEGV and DGEGV—Eigenvalues and, Optionally, the Eigenvectors of a Generalized Real Eigensystem, Az=wBz, where A and B Are Real General Matrices

These subroutines compute the eigenvalues and, optionally, the eigenvectors of a generalized real eigensystem, where **A** and **B** are real general matrices. Eigenvalues $w$ are based on the two parts returned in vectors **α** and **β**, such that $w_i = \alpha_i / \beta_i$ for **β**$_i$ ≠ 0, and $w_i = \infty$ for **β**$_i$ = 0. Eigenvectors are returned in matrix **Z**: $\mathbf{Az} = w\mathbf{Bz}$

**Table 133. Data Types**

| **A**, **B**, **β**, _aux_ | **α**, **Z** | Subroutine |
| :--- | :--- | :--- |
| Short-precision real | Short-precision complex | SGEGV^d |
| Long-precision real | Long-precision complex | DGEGV^d |

> d Not LAPACK. Although this subroutine has the same name as an existing LAPACK subroutine, its calling-sequence arguments and functionality are different from that LAPACK subroutine.

### Syntax

| Fortran | `CALL SGEGV \| DGEGV` (_iopt_, _a_, _lda_, _b_, _ldb_, _alpha_, _beta_, _z_, _ldz_, _n_, _aux_, _naux_) |
| :--- | :--- |
| C and C++ | `sgegv \| dgegv` (_iopt_, _a_, _lda_, _b_, _ldb_, _alpha_, _beta_, _z_, _ldz_, _n_, _aux_, _naux_); |

### On Entry:

- _iopt_
  - indicates the type of computation to be performed, where:
    - If _iopt_ = 0, eigenvalues only are computed.
    - If _iopt_ = 1, eigenvalues and eigenvectors are computed.
    - Specified as: a fullword integer; _iopt_ = 0 or 1.
- _a_
  - is the real general matrix **A** of order _n_.
    - Specified as: an _lda_ by (at least) _n_ array, containing numbers of the data type indicated in Table 133. On output, **A** is overwritten; that is, the original input is not preserved.
- _lda_
  - is the leading dimension of the array specified for _a_.
    - Specified as: a fullword integer; _lda_ > 0 and _lda_ ≥ _n_.
- _b_
  - is the real general matrix **B** of order _n_.
    - Specified as: an _ldb_ by (at least) _n_ array, containing numbers of the data type indicated in Table 133. On output, **B** is overwritten; that is, the original input is not preserved.
- _ldb_
  - is the leading dimension of the array specified for _b_.
    - Specified as: a fullword integer; _ldb_ > 0 and _ldb_ ≥ _n_.
- _alpha_
  - See “On Return” on page 732.
- _beta_
  - See “On Return” on page 732.
- _z_
  - See “On Return” on page 732.
- _ldz_
  - has the following meaning, where:
    - If _iopt_ = 0, it is not used in the computation.
