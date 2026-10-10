# SGEEV, DGEEV, CGEEV, and ZGEEV—Eigenvalues and, Optionally, All or Selected Eigenvectors of a General Matrix

SGEEV and DGEEV compute the eigenvalues and, optionally, all or selected eigenvectors of real general matrix *A*. CGEEV and ZGEEV compute the eigenvalues and, optionally, all or selected eigenvectors of complex general matrix *A*. Eigenvalues are returned in complex vector *w*, and eigenvectors are returned in complex matrix *Z*:

```
Az = wZ
```

*Table 130. Data Types*


| A | w, Z | aux | Subroutine |
| --- | --- | --- | --- |
| Short-precision real | Short-precision complex | Short-precision real | SGEEV4 |
| Long-precision real | Long-precision complex | Long-precision real | DGEEV4 |
| Short-precision complex | Short-precision complex | Short-precision real | CGEEV4 |
| Long-precision complex | Long-precision complex | Long-precision real | ZGEEV4 |


4Not LAPACK. Although this subroutine has the same name as an existing LAPACK subroutine, its calling-sequence arguments and functionality are different from that LAPACK subroutine.

# Syntax


| Fortran | CALL SGEEV \| DGEEV \| CGEEV \| ZGEEV (*iOpt, a, lda, w, z, ldz, select, n, aux, nAux*) |
| --- | --- |
| C and C++ | sGeev \| dGeev \| cGeev \| zGeev (*iOpt, a, lda, w, z, ldz, select, n, aux, nAux*); |


# On Entry:

*iOpt* indicates the type of computation to be performed, where:

+   If *iOpt* = 0, eigenvalues only are computed.
+   
+   If *iOpt* = 1, eigenvalues and eigenvectors are computed.
+   
+   If *iOpt* = 2, eigenvalues and eigenvectors corresponding to selected eigenvalues are computed.
+   
+   Specified as: a fullword integer; *iOpt* = 0, 1, or 2.

*a* is the real or complex general matrix *A* of order *n*, whose eigenvalues and, optionally, eigenvectors are computed. Specified as: an *lda* by (at least) *n* array, containing numbers of the data type indicated in Table 130. On output, A is overwritten; that is, the original input is not preserved.

*lda* is the leading dimension of the array specified for *a*.

Specified as: a fullword integer; *lda* > 0 and *lda* ≥ *n*.

*w*	See “On Return” on page 706.
*Z*	See “On Return” on page 706.

*ldz* has the following meaning, where:

+   If *iOpt* = 0, it is not used in the computation.
+   
+   If *iOpt* = 1 or 2, it is the leading dimension of the output array specified for z.
+   
+   Specified as: a fullword integer. It must have the following values, where:
+   
+   If *iOpt* = 0, *ldz* > 0.