# **SGEMM, DGEMM, CGEMM, and ZGEMM—Combined Matrix Multiplication and Addition for General Matrices, Their Transposes, or Conjugate Transposes**

SGEMM and DGEMM can perform any one of the following combined matrix computations, using scalars \( \alpha \) and \( \beta \), matrices \( A \) and \( B \) or their transposes, and matrix \( C \):

C \( \leftarrow \) \( \alpha AB+\beta C \)         C \( \leftarrow \) \( \alpha AB^T+\beta C \)

C \( \leftarrow \) \( \alpha A^TB+\beta C \)         C \( \leftarrow \) \( \alpha A^TB^T+\beta C \)

CGEMM and ZGEMM can perform any one of the following combined matrix computations, using scalars \( \alpha \) and \( \beta \), matrices \( A \) and \( B \), their transposes or their conjugate transposes, and matrix \( C \):

C \( \leftarrow \) \( \alpha AB+\beta C \)          C \( \leftarrow \) \( \alpha AB^T+\beta C \)       C \( \leftarrow \) \( \alpha AB^{H}+\beta C \)

C \( \leftarrow \) \( \alpha A^TB+\beta C \)        C \( \leftarrow \) \( \alpha A^TB^T+\beta C \)      C \( \leftarrow \) \( \alpha A^TB^{H}+\beta C \)

C \( \leftarrow \) \( \alpha A^{H}B+\beta C \)      C \( \leftarrow \) \( \alpha A^{H}B^T+\beta C \)   C \( \leftarrow \) \( \alpha A^{H}B^{H}+\beta C \)

Table 80. Data Types

| A, B, C, \( \alpha \), \( \beta \)      | Subroutine |
|-----------------------------|------------|
| Short-precision real        | SGEMM      |
| Long-precision real        | DGEMM      |
| Short-precision complex     | CGEMM      |
| Long-precision complex      | ZGEMM      |

# Syntax

| **Fortran** | CALL SGEMM \| DGEMM \| CGEMM \| ZGEMM (transa, transb, l, n, m, alpha, a, lda, b, ldb, beta, c, ldc) |
|----|----|
| **C and C++** | sgemm \| dgem \| cgem \| zgem (transa, transb, l, n, m, alpha, a, lda, b, ldb, beta, c, ldc); |

**On Entry:**

*transa* indicates the form of matrix A to use in the computation, where:

- If transa = 'N', A is used in the computation.
- If transa = 'T', \( A^{T} \) is used in the computation.
- If transa = 'C', \( A^{H} \) is used in the computation.

Specified as: a single character; transa = 'N', T', or 'C'.

*transb* indicates the form of matrix B to use in the computation, where:

- If transb = 'N', B is used in the computation.
- If transb = 'T', \( B^{T} \) is used in the computation.
- If transb = 'C', \( B^{H} \) is used in the computation.

Specified as: a single character; transb = 'N', T', or 'C'.

l is the number of rows in matrix C.

Specified as: a fullword integer; 0 \( \leq l \leq ldc \).