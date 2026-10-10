# DSDMX—Matrix-Vector Product for a Sparse Matrix or Its Transpose in Compressed-Diagonal Storage Mode

This subprogram computes the matrix-vector product for square sparse matrix $A$, stored in compressed-diagonal storage mode, using either the matrix or its transpose, and vectors $x$ and $y$:
$\begin{array}{c}y = Ax \\ y = A^T x\end{array}$
where $A$, $x$, and $y$ contain long-precision real numbers.

# Syntax

| Fortran | C and C++ |
| :------- | :--------- |
| `CALL DSDMX (iopt, n, nd, ad, lda, trans, la, x, y)` | `dsdmx (iopt, n, nd, ad, lda, trans, la, x, y);` |

# On Entry:

**iopt**
indicates the storage variation used for sparse matrix $A$, stored in compressed-diagonal storage mode, where:
If *iopt* = 0, matrix $A$ is a general sparse matrix, where all the nonzero diagonals in matrix $A$ are used to set up the storage arrays.
If *iopt* = 1, matrix $A$ is a symmetric sparse matrix, where only the nonzero main diagonal and one of each of the unique nonzero diagonals are used to set up the storage arrays.
Specified as: a fullword integer; *iopt* = 0 or 1.

**n**
is the order of sparse matrix $A$ and the number of elements in vectors $x$ and $y$. Specified as: a fullword integer; $n \ge 0$.

**nd**
is the number of diagonals stored in the columns of array AD, as well as the number of columns in AD and the number of elements in array LA.
Specified as: a fullword integer; $nd \ge 0$.

**ad**
is the sparse matrix $A$ of order $n$, stored in compressed diagonal storage in an array, referred to as AD. The *iopt* argument indicates the storage variation used for storing matrix $A$. The *trans* argument indicates the following:
If *trans* = 'N', $A$ is used in the computation.
If *trans* = 'T', $A^T$ is used in the computation.
**Note:** No data should be moved to form $A^T$; that is, the matrix $A$ should always be stored in its untransposed form.
Specified as: an $lda$ by (at least) $nd$ array, containing long-precision real numbers; $lda \ge n$.

**lda**
is the size of the leading dimension of the array specified for $ad$. Specified as: a fullword integer; $lda > 0$ and $lda \ge n$.

**trans**
indicates the form of matrix $A$ to use in the computation, where:
If *trans* = 'N', $A$ is used in the computation.
If *trans* = 'T', $A^T$ is used in the computation.
Specified as: a single character; *trans* = 'N' or 'T'.