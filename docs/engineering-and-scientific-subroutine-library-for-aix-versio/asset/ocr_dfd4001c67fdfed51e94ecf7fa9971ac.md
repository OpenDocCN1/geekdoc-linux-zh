# SPPFCD, DPPFCD, SPOFCD, and DPOFCD—Positive Definite Real Symmetric Matrix Factorization, Condition Number Reciprocal, and Determinant

The SPPFCD and DPPFCD subroutines factor positive definite symmetric matrix *A*, stored in lower-packed storage mode, using Gaussian elimination ($LL^T$). The reciprocal of the condition number and the determinant of matrix *A* can also be computed. To solve the system of equations with one or more right-hand sides, follow the call to these subroutines with one or more calls to SPPS or DPPS, respectively.

The SPOFCD and DPOFCD subroutines factor positive definite symmetric matrix *A*, stored in upper or lower storage mode, using Cholesky factorization ($LL^T$ or $U^TU$). The reciprocal of the condition number and the determinant of matrix *A* can also be computed. To solve the system of equations with one or more right-hand sides, follow the call to these subroutines with a call to SPOM or DPOSM, respectively. To find the inverse of matrix *A*, follow the call to these subroutines with a call to SPOICD or DPOICD, respectively.

# Table 103. Data Types

| *A*, aux, rcond, det | Subroutine |
|---|---|
| Short-precision real | SPPFCD and SPOFCD |
| Long-precision real | DPPFCD and DPOFCD |

Note: The output factorization from SPPFCD and DPPFCD should be used only as input to the solve subroutines SPPS and DPPS, respectively. The output from SPOFCD and DPOFCD should be used only as input to the following subroutines for performing a solve or inverse: SPOMS/SPOICD and DPOMS/DPOICD, respectively.

# Syntax

| Fortran | CALL SPPFCD | DPPFCD (*ap, n, iopt, rcond, det, aux, naux*)
CALL SPOFCD | DPOFCD (*uplo, a, lda, n, iopt, rcond, det, aux, naux*) |
| C and C++ | sppfcd | dppfcd (*ap, n, iopt, rcond, det, aux, naux*);
spofcd | dpofcd (*uplo, a, lda, n, iopt, rcond, det, aux, naux*); |

# On Entry:

+   *uplo* indicates whether matrix *A* is stored in upper or lower storage mode, where:
+   - If *uplo* = 'U', *A* is stored in upper storage mode.
+   - If *uplo* = 'L', *A* is stored in lower storage mode.
+   - Specified as: a single character. It must be 'U' or 'L'.
+   *ap* is the array, referred to as *AP*, in which the matrix *A*, to be factored, is stored in lower-packed storage mode.
+   - Specified as: a one-dimensional array of (at least) length $n(n+1)/2+n$, containing numbers of the data type indicated in Table 103.
+   *a* is the positive definite symmetric matrix *A*, to be factored.