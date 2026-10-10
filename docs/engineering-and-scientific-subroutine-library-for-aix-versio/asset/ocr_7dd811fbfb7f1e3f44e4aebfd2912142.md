# STRSV, DTRSV, CTRSV, ZTRSV, STPSV, DTPSV, CTPSV, and ZTPSV

STRSV, DTRSV, STPSV, and DTPSV perform one of the following solves for a triangular system of equations with a single right-hand side, using the vector $x$ and triangular matrix $A$ or its transpose:

| Solution | Equation |
| --- | --- |
| 1. $x\leftarrow A^{-1}x$ | $Ax = b$ |
| 2. $x\leftarrow A^{T-1}x$ | $A^{T}x = b$ |

CTRSV, ZTRSV, CTPSV, and ZTPSV perform one of the following solves for a triangular system of equations with a single right-hand side, using the vector $x$ and triangular matrix $A$, its transpose, or its conjugate transpose:

| Solution | Equation |
| --- | --- |
| 1. $x\leftarrow A^{-1}x$ | $Ax = b$ |
| 2. $x\leftarrow A^{T-1}x$ | $A^{T}x = b$ |
| 3. $x\leftarrow A^{H-1}x$ | $A^{H}x = b$ |

Matrix $A$ can be either upper or lower triangular, where:

+   - For the \_TRSV subroutines, it is stored in upper- or lower-triangular storage mode, respectively.
+   - For the \_TPSV subroutines, it is stored in upper- or lower-triangular-packed storage mode, respectively.

> **Note:** The term $b$ used in the systems of equations listed above represents the right-hand side of the system. It is important to note that in these subroutines the right-hand side of the equation is actually provided in the input-output argument $x$.

Table 109. Data Types

| $A$, $x$ | Subroutine |
| --- | --- |
| Short-precision real | STRSV and STPSV |
| Long-precision real | DTRSV and DTPSV |
| Short-precision complex | CTRSV and CTPSV |
| Long-precision complex | ZTRSV and ZTPSV |

# Syntax

```
```
Fortran      CALL STRSV | DTRSV | CTRSV | ZTRSV (uplo, transa, diag, n, a, lda, x, incx)
              CALL STPSV | DTPSV | CTPSV | ZTPSV (uplo, transa, diag, n, ap, x, incx)

C and C++    strsv | dtrsv | ctrsv | ztrsv (uplo, transa, diag, n, a, lda, x, incx);
             stpsv | dtpsv | ctpsv | ztpsv (uplo, transa, diag, n, ap, x, incx);
```
```

# On Entry:

$uplo$ indicates whether matrix $A$ is an upper or lower triangular matrix, where: If $uplo = 'U'$, $A$ is an upper triangular matrix.