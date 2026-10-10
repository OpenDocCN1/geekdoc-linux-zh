# ## DSDCG—Sparse Positive Definite or Negative Definite Symmetric Matrix Iterative Solve Using Compressed-Diagonal Storage Mode

This subroutine solves a symmetric, positive definite or negative definite linear system, using the two-term conjugate gradient method, with or without preconditioning by an incomplete Cholesky factorization, for a sparse matrix stored in compressed-diagonal storage mode. Matrix $A$ and vectors $x$ and $b$ are used:
$Ax = b$
where $A$, $x$, and $b$ contain long-precision real numbers.

# ### Syntax

| Fortran | CALL DSDCG (iopt, m, nd, ad, lda, la, b, x, iparm, rparm, aux1, naux1, aux2, naux2) |
|---|---|
| C and C++ | dscg (iopt, m, nd, ad, lda, la, b, x, iparm, rparm, aux1, naux1, aux2, naux2); |

# ### On Entry:

*iopt* indicates the type of storage used, where:

If *iopt = 0*, all the nonzero diagonals of the sparse matrix are stored in compressed-diagonal storage mode.

If *iopt = 1*, the sparse matrix, stored in compressed-diagonal storage mode, is symmetric. Only the main diagonal and one of each pair of identical diagonals are stored in array $AD$.

Specified as: a fullword integer; *iopt = 0 or 1*.

*m* is the order of the linear system $Ax = b$ and the number of rows in sparse matrix $A$.

Specified as: a fullword integer; *m ≥ 0*.

*nd* is the number of nonzero diagonals stored in the columns of array $AD$, the number of columns in the array $AD$, and the number of elements in array $LA$.

Specified as: a fullword integer; it must have the following value, where:

If *m > 0*, then *nd > 0*.

If *m = 0*, then *nd ≥ 0*.

*ad* is the array, referred to as $AD$, containing the values of the nonzero elements of the sparse matrix stored in compressed-diagonal storage mode.

If *iopt = 1*, the main diagonal and one of each pair of identical diagonals is stored in this array.

Specified as: an *lda* by (at least) *nd* array, containing long-precision real numbers.

*lda* is the leading dimension of the array specified for *ad*.

Specified as: a fullword integer; *lda > 0* and *lda ≥ m*.

*la* is the array, referred to as $LA$, containing the diagonal numbers $k$ for the diagonals stored in each corresponding column in array $AD$. For an explanation of how diagonal numbers are assigned, see “Compressed-Diagonal Storage Mode” on page 91.

Specified as: a one-dimensional array of (at least) length *nd*, containing fullword integers, where $1-m ≤$ (elements of $LA$) $≤ m-1$.