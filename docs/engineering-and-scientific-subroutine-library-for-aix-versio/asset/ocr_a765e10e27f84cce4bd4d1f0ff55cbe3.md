# **SPTS and DPTS—Positive Definite Symmetric Tridiagonal Matrix Solve**

These subroutines solve a positive definite symmetric tridiagonal system of equations using the factorization of matrix $A$, stored in symmetric-tridiagonal storage mode, produced by SPTF and DPTF, respectively.

| $c, d, b, x$ | Subroutine |
| --- | --- |
| Short-precision real | SPTS |
| Long-precision real | DPTS |

**Note:** The input to these solve subroutines must be the output from the factorization subroutines SPTF and DPTF, respectively.

# ### Syntax

| Fortran | CALL SPTS \| DPTS ($n, c, d, bx$) |
| --- | --- |
| C and C++ | spts \| dpts ($n, c, d, bx$); |

+   On Entry:
+   
+   *   $n$ is the order $n$ of tridiagonal matrix $A$. Specified as: a fullword integer, $n \geq 0$.
+   *   $c$ is the vector $c$, containing part of the factorization of matrix $A$ from SPTF or DPTF, respectively, in an array, referred to as C. Specified as: a one-dimensional array of (at least) length $n$, containing numbers of the data type indicated in Table 122.
+   *   $d$ is the vector $d$, containing part of the factorization of matrix $A$ from SPTF or DPTF, respectively, in an array, referred to as D. Specified as: a one-dimensional array of (at least) length $n$, containing numbers of the data type indicated in Table 122.
+   *   $bx$ is the vector $b$, containing the right-hand side of the system in the first $n$ positions in an array, referred to as BX. Specified as: a one-dimensional array of (at least) length $n$, containing numbers of the data type indicated in Table 122.

+   On Return:
+   
+   *   $bx$ is the solution vector $x$ of length $n$, containing the solution of the tridiagonal system in the first $n$ positions in an array, referred to as BX. Returned as: a one-dimensional array of (at least) length $n$, containing numbers of the data type indicated in Table 122.

**Note**

For a description of how tridiagonal matrices are stored, see “Positive Definite or Negative Definite Symmetric Matrix” on page 69.

**Function**

The solution of positive definite symmetric tridiagonal system $Ax = b$ is computed using the factorization produced by SPTF or DPTF, respectively. The factorization is based on Gaussian elimination. See reference [79].