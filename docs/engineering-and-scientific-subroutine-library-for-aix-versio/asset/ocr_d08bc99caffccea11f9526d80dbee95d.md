# **SSBMV, DSBMV, CHBMV, and ZHBMV—Matrix-Vector Product for a Real Symmetric or Complex Hermitian Band Matrix**

SSBMV and DSBMV compute the matrix-vector product for a real symmetric band matrix. CHBMV and ZHBMV compute the matrix-vector product for a complex Hermitian band matrix. The band matrix *A* is stored in either upper- or lower-band-packed storage mode. It uses the scalars *α* and *β*, vectors *x* and *y*, and band matrix *A*:

*y* ← *β**y* + *αAx*
*y* ← *β**y* + *αAx*

**Table 72. Data Types**

| *α*, *β*, *x*, *y*, *A* | Subprogram |
| :--- | :--- |
| Short-precision real | SSBMV |
| Long-precision real | DSBMV |
| Short-precision complex | CHBMV |
| Long-precision complex | ZHBMV |

# **Syntax**

| Fortran | C and C++ |
| :--- | :--- |
| `CALL SSBMV \| DSBMV \| CHBMV \| ZHBMV (uplo, n, k, alpha, a, lda, x, incx, beta, y, incy)` | `ssbmv \| dsbmv \| chbmv \| zhbmv (uplo, n, k, alpha, a, lda, x, incx, beta, y, incy);` |

**On Entry:**

+   *uplo*
+   : indicates the storage mode used for matrix *A*, where either the upper or lower triangle can be stored:
+       - If *uplo* = 'U', *A* is stored in upper-band-packed storage mode.
+       - If *uplo* = 'L', *A* is stored in lower-band-packed storage mode.
+       - Specified as: a single character. It must be 'U' or 'L'.

+   *n*
+   : is the order of matrix *A* and the number of elements in vectors *x* and *y*.
+   - Specified as: a fullword integer; *n* ≥ 0.

+   *k*
+   : is the half band width *k* of the matrix *A*.
+   - Specified as: a fullword integer; *k* ≥ 0.

+   *alpha*
+   : is the scaling constant *α*.
+   - Specified as: a number of the data type indicated in Table 72.

+   *a*
+   : is the real symmetric or complex Hermitian band matrix *A* of order *n*, having a half band width of *k*, where:
+   - If *uplo* = 'U', *A* is stored in upper-band-packed storage mode.
+   - If *uplo* = 'L', *A* is stored in lower-band-packed storage mode.
+   - Specified as: an *lda* by (at least) *n* array, containing numbers of the data type indicated in Table 72, where *lda* ≥ *k*+1.

+   *lda*
+   : is the leading dimension of the array specified for *a*.
+   - Specified as: a fullword integer; *lda* > 0 and *lda* ≥ *k*+1.

+   *x*
+   : is the vector *x* of length *n*.