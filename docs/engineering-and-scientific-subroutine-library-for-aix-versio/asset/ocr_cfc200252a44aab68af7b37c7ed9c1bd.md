# ## DSDGCG—General Sparse Matrix Iterative Solve Using
## Compressed-Diagonal Storage Mode

This subroutine solves a general sparse linear system of equations using an iterative algorithm, conjugate gradient squared or generalized minimum residual, with or without preconditioning by an incomplete LU factorization. The subroutine is suitable for positive real matrices—that is, when the symmetric part of the matrix, (A+A$^{\text{T}}$)/2, is positive definite. The sparse matrix is stored in compressed-diagonal storage mode. Matrix **A** and vectors **x** and **b** are used: **Ax = b** where **A**, **x**, and **b** contain long-precision real numbers.

# ### Syntax

| | |
| :--- | :--- |
| **Fortran** | CALL DSDGCG (m, nd, ad, lda, la, b, x, iparm, rparm, auxl, naux1, aux2, naux2) |
| **C and C++** | dsdgcg (m, nd, ad, lda, la, b, x, iparm, rparm, auxl, naux1, aux2, naux2); |

# **On Entry:**

+   -   ***m***
+       is the order of the linear system **Ax = b** and the number of rows in sparse matrix **A**.
+       Specified as: a fullword integer; *m* $\ge$ 0.
+   -   ***nd***
+       is the number of nonzero diagonals stored in the columns of array **AD**, the number of columns in array **AD**, and the number of elements in array **LA**.
+       Specified as: a fullword integer; it must have the following value, where:
+       If *m* $>$ 0, then *nd* $>$ 0.
+       If *m* = 0, then *nd* $\ge$ 0.
+   -   ***ad***
+       is the array, referred to as **AD**, containing the values of the nonzero elements of the sparse matrix, stored in compressed-matrix storage mode.
+       Specified as: an *lda* by (at least) *nd* array, containing long-precision real numbers.
+   -   ***lda***
+       is the leading dimension of the arrays specified for *ad*.
+       Specified as: a fullword integer; *lda* $>$ 0 and *lda* $\ge$ *m*.
+   -   ***la***
+       is the array, referred to as **LA**, containing the diagonal numbers *k* for the diagonals stored in each corresponding column in array **AD**. For an explanation of how diagonal numbers are stored, see “Compressed-Diagonal Storage Mode” on page 91.
+       Specified as: a one-dimensional array of (at least) length *nd*, containing fullword integers, where 1 $-$ *m* $\le$ (elements of **LA**) $\le$ (*m*$-$$ 1$).
+   -   ***b***
+       is the vector *b* of length *m*, containing the right-hand side of the matrix problem.
+       Specified as: a one-dimensional array of (at least) length *m*, containing long-precision real numbers.
+   -   ***x***
+       is the vector *x* of length *m*, containing your initial guess of the solution of the linear system.