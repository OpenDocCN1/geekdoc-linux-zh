SSYRK, DSYRK, CSYRK, ZSYRK, CHERK, and ZHERK

# ## SSYRK, DSYRK, CSYRK, ZSYRK, CHERK, and ZHERK—Rank-K Update of a Real or Complex Symmetric or a Complex Hermitian Matrix

These subroutines compute one of the following rank-k updates, where matrix *C* is stored in either upper or lower storage mode. SSYRK, DSYRK, CSYRK, and ZSYRK use the scalars $\alpha$ and $\beta$, real or complex matrix *A* or its transpose, and real or complex symmetric matrix *C* to compute:

+   1.  $C \leftarrow \alpha A A^{T} + \beta C$
+   2.  $C \leftarrow \alpha A^{T} A + \beta C$

CHERK and ZHERK use the scalars $\alpha$ and $\beta$, complex matrix *A* or its complex conjugate transpose, and complex Hermitian matrix *C* to compute:

+   3.  $C \leftarrow \alpha A A^{H} + \beta C$
+   4.  $C \leftarrow \alpha A^{H} A + \beta C$

*Table 83. Data Types*

| A, C | $\alpha$, $\beta$ | Subprogram |
|:---------------------------|:------------------------|:------------|
| Short-precision real | Short-precision real | SSYRK |
| Long-precision real | Long-precision real | DSYRK |
| Short-precision complex | Short-precision complex | CSYRK |
| Long-precision complex | Long-precision complex | ZSYRK |
| Short-precision complex | Short-precision real | CHERK |
| Long-precision complex | Long-precision real | ZHERK |

# ## Syntax

| **Fortran** | CALL SSYRK | DSYRK | CSYRK | ZSYRK | CHERK | ZHERK (*uplo*, *trans*, *n*, *k*, *alpha*, *a*, *lda*,
| beta, *c*, *ldc*) |
| **C and C++** | ssyrk | dsyrk | csyrk | zsyrk | cherk | zherk (*uplo*, *trans*, *n*, *k*, *alpha*, *a*, *lda*, *beta*, *c*, *ldc*); |

# ### On Entry:

*uplo* indicates the storage mode used for matrix *C*, where:

If *uplo* = 'U', *C* is stored in upper storage mode.

If *uplo* = 'L', *C* is stored in lower storage mode.

Specified as: a single character. It must be 'U' or 'L'.

*trans* indicates the form of matrix *A* to use in the computation, where:

If *trans* = 'N', *A* is used, resulting in equation 1 or 3.

If *trans* = 'T', *A*^{T} is used, resulting in equation 2.

If *trans* = 'C', *A*^{H} is used, resulting in equation 4.

Specified as: a single character, where:

For SSYRK and DSYRK, it must be 'N', 'T', or 'C'.

For CSYRK and ZSYRK, it must be 'N' or 'T'.

For CHERK and ZHERK, it must be 'N' or 'C'.

*n* is the order of matrix *C*.

Specified as: a fullword integer; $0 \leq n \leq ldc$ and: