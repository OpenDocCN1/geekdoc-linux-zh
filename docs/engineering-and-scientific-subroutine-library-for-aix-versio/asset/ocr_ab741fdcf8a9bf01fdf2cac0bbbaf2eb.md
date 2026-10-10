# SGEMV, DGEMV, CGEMV, ZGEMV, SGEMX, DGEMX, SGETX, and DGETX

SGEMV and DGEMV compute the matrix-vector product for either a real general matrix or its transpose, using the scalars $\alpha$ and $\beta$, vectors $\boldsymbol{x}$ and $\boldsymbol{y}$, and matrix $\boldsymbol{A}$ or its transpose:
\[
\boldsymbol{y} \leftarrow \beta \boldsymbol{y}+\alpha \boldsymbol{A} \boldsymbol{x}
\]
\[
\boldsymbol{y} \leftarrow \beta \boldsymbol{y}+\alpha \boldsymbol{A}^{\mathrm{T}} \boldsymbol{x}
\]

CGEMV and ZGEMV compute the matrix-vector product for either a complex general matrix, its transpose, or its conjugate transpose, using the scalars $\alpha$ and $\beta$, vectors $\boldsymbol{x}$ and $\boldsymbol{y}$, and matrix $\boldsymbol{A}$, its transpose, or its conjugate transpose:
\[
\boldsymbol{y} \leftarrow \beta \boldsymbol{y}+\alpha \boldsymbol{A} \boldsymbol{x}
\]
\[
\boldsymbol{y} \leftarrow \beta \boldsymbol{y}+\alpha \boldsymbol{A}^{\mathrm{T}} \boldsymbol{x}
\]
\[
\boldsymbol{y} \leftarrow \beta \boldsymbol{y}+\alpha \boldsymbol{A}^{\mathrm{H}} \boldsymbol{x}
\]

SGEMX and DGEMX compute the matrix-vector product for a real general matrix, using the scalar $\alpha$, vectors $\boldsymbol{x}$ and $\boldsymbol{y}$, and matrix $\boldsymbol{A}$:
\[
\boldsymbol{y} \leftarrow \boldsymbol{y}+\alpha \boldsymbol{A} \boldsymbol{x}
\]

SGETX and DGETX compute the matrix-vector product for the transpose of a real general matrix, using the scalar $\alpha$, vectors $\boldsymbol{x}$ and $\boldsymbol{y}$, and the transpose of matrix $\boldsymbol{A}$:
\[
\boldsymbol{y} \leftarrow \boldsymbol{y}+\alpha \boldsymbol{A}^{\mathrm{T}} \boldsymbol{x}
\]

**Table 66. Data Types**

|  $\alpha$, $\beta$, $\boldsymbol{x}$, $\boldsymbol{y}$, $\boldsymbol{A}$ | Subprogram |
|:--------------------------:|:-------------------------:|
|      Short-precision real | SGEMV, SGEMX, and SGETX   |
|      Long-precision real  | DGEMV, DGEMX, and DGETX   |
|   Short-precision complex  |            CGEMV          |
|    Long-precision complex  |            ZGEMV          |

**Note:** SGEMV and DGEMV are Level 2 BLAS subroutines. It is suggested that these subroutines be used instead of SGEMX, DGEMX, SGETX, and DGETX, which are provided only for compatibility with earlier releases of ESSL.

# **Syntax**


|  | |
|---|---|
| **Fortran** | CALL SGEMV \| DGEMV \| CGEMV \| ZGEMV (*transa, m, n, alpha, a, lda, x, incx, beta, y, incy*) |
| | CALL SGEMX \| DGEMX \| SGETX \| DGETX (*m, n, alpha, a, lda, x, incx, y, incy*) |
| **C and C++** | sgemv \| dgemv \| cgemv \| zgemv (*transa, m, n, alpha, a, lda, x, incx, beta, y, incy*); |
| | sgemx \| dgemx \| sgmtx \| dgmtx (*m, n, alpha, a, lda, x, incx, y, incy*); |


# **On Entry:**

*transa*  indicates the form of matrix $\boldsymbol{A}$ to use in the computation, where:
If *transa* = '`N`', $\boldsymbol{A}$ is used in the computation.
If *transa* = '`T`', $\boldsymbol{A}^{\mathrm{T}}$ is used in the computation.