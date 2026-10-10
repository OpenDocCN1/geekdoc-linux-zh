
If $IPARM(3) = -10$, *aux2* is unchanged.

See “Notes” for additional information on *aux2*. Returned as: an area of storage, containing long-precision real numbers.

## Notes

1. When $IPARM(3) = -10$, this subroutine uses the incomplete $LU$ factorization in *aux2*, computed in an earlier call to this subroutine. When $IPARM(3) = 10$, this subroutine stores the incomplete $LU$ factorization and stores it in *aux2*.
2. If you solve the same sparse linear system of equations several times with different right-hand sides using the preconditioned algorithm, specify $IPARM(2) = 10$ on the first invocation. The incomplete factorization is stored in *aux2*. You may save computing time on subsequent calls by setting $IPARM(3)$ equal to $-10$. In this way, the algorithm reutilizes the incomplete factorization that was computed the first time. Therefore, you should not modify the contents of *aux2* between calls.
3. Matrix $A$ must have no common elements with vectors $x$ and $b$; otherwise, results are unpredictable.
4. In the iterative solvers for sparse matrices, the relative accuracy $\epsilon$ ($RPARM(1)$) must be specified “reasonably” ($10^{-4}$ to $10^{-3}$). The algorithm computes a sequence of approximate solution vectors $x$ that converge to the solution. The iterative procedure is stopped when the norm of the residual is sufficiently small—that is, when: $||b - Ax||_2 / ||x||_2 < \epsilon$

As a result, if you specify a larger $\epsilon$, the algorithm takes fewer iterations to converge to a solution. If you specify a smaller $\epsilon$, the algorithm requires more iterations and computer time, but converges to a more precise solution. If the value you specify is unreasonably small, the algorithm may fail to converge within the number of iterations it is allowed to perform.

5. For a description of how sparse matrices are stored in compressed-matrix storage mode, see “Compressed-Matrix Storage Mode” on page 90.
6. On output, array $AC$ is not bitwise identical to what it was on input because the matrix $A$ is scaled before starting the iterative process and is unscaled before returning control to the user.
7. You have the option of having the minimum required value for *nux* dynamically returned to your program. For details, see “Using Auxiliary Storage in ESSL” on page 32.

## Function

The linear system: $Ax = b$

is solved using either the conjugate gradient squared method or the generalized minimum residual method, with or without preconditioning by an incomplete $LU$ factorization, where:

- $A$ is a sparse matrix of order $m$, stored in compressed-matrix storage mode in arrays $AC$ and $KA$.
- $x$ is a vector of length $m$.
- $b$ is a vector of length $m$.

See references [89] and [91]. [38].

If your program uses a sparse matrix stored by rows and you want to use this subroutine, first convert your sparse matrix to compressed-matrix storage mode by using the subroutine DSRSM described on page 972.

# Error Conditions

**Resource Errors:** Error 2015 is unrecoverable, *naux1* = 0, and unable to allocate work area.

**Computational Errors:** The following errors, with their corresponding return codes, can occur in this subroutine. For details on error handling, see “What Can You Do about ESSL Computational Errors?” on page 47.

- For error 2110, return code 1 indicates that the subroutine exceeded IPARM(1) iterations without converging. Vector $\boldsymbol{x}$ contains the approximate solution computed at the last iteration.
- For error 2111, return code 2 indicates that $aux2$ contains an incorrect factorization. The subroutine has been called with IPARM(3) = $-10$, and $aux2$ contains an incomplete factorization of the input matrix $A$ that was computed by a previous call to the subroutine when IPARM(3) = 10. This error indicates that $aux2$ has been modified since the last call to the subroutine, or that the input matrix is not the same as the one that was factored. If the default action has been overridden, the subroutine can be called again with the same parameters, with the exception of IPARM(3) = 0 or 10.
- For error 2112, return code 3 indicates that the incomplete LU factorization of $A$ could not be completed, because one pivot was 0.
- For error 2116, return code 4 indicates that the matrix is singular, because all elements in one row of the matrix contain 0. Array $\mathbf{AC}$ is partially modified and does not represent the same matrix as on entry.

**Input-Argument Errors:**

1. $m < 0$
2. $lda < 1$
3. $lda < m$
4. $nz < 0$
5. $nz = 0$ and $m > 0$
6. IPARM(1) $< 0$
7. IPARM(2) $< 0$
8. IPARM(3) $\neq 0, 10$, or $-10$
9. RPARM(1) $< 0$
10. RPARM(2) $< 0$
11. Error 2015 is recoverable or *naux1*$\neq$0, and *naux1* is too small — that is, less than the minimum required value. Return code 5 is returned if error 2015 is recoverable.
12. *naux2* is too small — that is, less than the minimum required value. Return code 5 is returned if error 2015 is recoverable.

## Example 1

This example finds the solution of the linear system $A\mathbf{x} = \mathbf{b}$ for the sparse matrix $A$, which is stored in compressed-matrix storage mode in arrays $\mathbf{AC}$ and $\mathbf{KA}$. The system is solved using the conjugate gradient squared method. Matrix $A$ is:

| 2.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 0.0 | 2.0 | -1.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 |
| 0.0 | 1.0 | 2.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 |
| 1.0 | 0.0 | 0.0 | 2.0 | -1.0 | 0.0 | 0.0 | 0.0 | 0.0 |
| 0.0 | 0.0 | 0.0 | 1.0 | 2.0 | -1.0 | 0.0 | 0.0 | 0.0 |
| 0.0 | 0.0 | 0.0 | 0.0 | 1.0 | 2.0 | -1.0 | 0.0 | 0.0 |
| 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 1.0 | 2.0 | -1.0 | 0.0 |

# **DSMCGG**

![](img/5b0f44f3be6048723819b26aed7f6f03_689_0.png)

**Note**: For input matrix KA, (.) indicates any value between 1 and 9.

**Call Statement and Input**:

```
M   NZ   AC    KA    LDA   B     X     IPARM   RPARAM  AUX1    NAUX1   AUX2    NAUX2
|    |     |     |     |     |     |     |       |       |       |       |       |       |
CALL DSMCG( 9 ,  3 , AC , KA ,  9 ,  B , X , IPARM , RPARAM , AUX1 ,  63  , AUX2 ,  0  )

IPARM(1)  =  20
IPARM(2)  =   0
IPARM(3)  =   0
RPARM(1)  = 1.0-7
```

![](img/5b0f44f3be6048723819b26aed7f6f03_689_1.png)

![](img/5b0f44f3be6048723819b26aed7f6f03_689_2.png)

```
B     = (2.0, 1.0, 3.0, 2.0, 2.0, 2.0, 2.0, 2.0, 3.0)
X     = (0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0)
```

**Output**:

```
X       = (1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0)
IPARM(4)  =   9
RPARM(3)  = 0.150D-19
```

## Example 2

This example finds the solution of the linear system $\mathbf{A}\mathbf{x} = \mathbf{b}$ for the same sparse matrix **A** as in Example 1, which is stored in compressed-matrix storage mode in arrays **AC** and **KA**. The system is solved using the generalized minimum residual method, restarted after 5 steps and preconditioned with an incomplete LU factorization. Most of the input is the same as in Example 1.

**Note**: For input matrix KA, ( . ) indicates any value between 1 and 9.

**Call Statement and Input**:

```
M    NZ    AC     KA    LDA    B      X      IPARM    RPARAM   AUX1    NAUX1   AUX2    NAUX2
|     |      |     |      |     |      |      |        |        |       |       |       |       |
CALL DSMCG( 9 ,  3 , AC , KA ,  9 ,  B , X , IPARM , RPARAM , AUX1 ,  109  , AUX2 ,  46  )
```

```
IPARM(1) = 20
IPARM(2) = 5
IPARM(3) = 10
RPARM(1) = 1.0-7
AC = (same as input AC in Example 1)
KA = (same as input KA in Example 1)
B = (2.0, 1.0, 3.0, 2.0, 2.0, 2.0, 2.0, 3.0)
X = (0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0)
```

**Output:**

```
X = (1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0)
IPARM(4) = 2
RPARM(3) = 0.290D-15
```

# DSDGCG—General Sparse Matrix Iterative Solve Using Compressed-Diagonal Storage Mode

This subroutine solves a general sparse linear system of equations using an iterative algorithm, conjugate gradient squared or generalized minimum residual, with or without preconditioning by an incomplete LU factorization. The subroutine is suitable for positive real matrices—that is, when the symmetric part of the matrix, (A+A$^{\text{T}}$)/2, is positive definite. The sparse matrix is stored in compressed-diagonal storage mode. Matrix **A** and vectors **x** and **b** are used: **Ax = b** where **A**, **x**, and **b** contain long-precision real numbers.

### Syntax

| Language | Syntax |
| :--- | :--- |
| **Fortran** | CALL DSDGCG (m, nd, ad, lda, la, b, x, iparm, rparm, aux1, naux1, aux2, naux2) |
| **C and C++** | dsdgcg (m, nd, ad, lda, la, b, x, iparm, rparm, aux1, naux1, aux2, naux2); |

**On Entry:**

- ***m*** is the order of the linear system **Ax = b** and the number of rows in sparse matrix **A**. Specified as: a fullword integer; *m* $\ge$ 0.
- ***nd*** is the number of nonzero diagonals stored in the columns of array **AD**, the number of columns in array **AD**, and the number of elements in array **LA**. Specified as: a fullword integer; it must have the following value, where: If *m* $>$ 0, then *nd* $>$ 0. If *m* = 0, then *nd* $\ge$ 0.
- ***ad*** is the array, referred to as **AD**, containing the values of the nonzero elements of the sparse matrix, stored in compressed-matrix storage mode. Specified as: an *lda* by (at least) *nd* array, containing long-precision real numbers.
- ***lda*** is the leading dimension of the arrays specified for *ad*. Specified as: a fullword integer; *lda* $>$ 0 and *lda* $\ge$ *m*.
- ***la*** is the array, referred to as **LA**, containing the diagonal numbers *k* for the diagonals stored in each corresponding column in array **AD**. For an explanation of how diagonal numbers are stored, see “Compressed-Diagonal Storage Mode” on page 91. Specified as: a one-dimensional array of (at least) length *nd*, containing fullword integers, where 1 $-$ *m* $\le$ (elements of **LA**) $\le$ (*m*$-1*).
- ***b*** is the vector *b* of length *m*, containing the right-hand side of the matrix problem. Specified as: a one-dimensional array of (at least) length *m*, containing long-precision real numbers.
- ***x*** is the vector *x* of length *m*, containing your initial guess of the solution of the linear system.
