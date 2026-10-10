# SSWAP, DSWAP, CSWAP, and ZSWAP—Interchange the Elements of Two Vectors

These subprograms interchange the elements of vectors $x$ and $y$.

$y \leftrightarrow x$

Table 55. Data Types

| x, y | Subprogram |
| :--- | :--- |
| Short-precision real | SSWAP |
| Long-precision real | DSWAP |
| Short-precision complex | CSWAP |
| Long-precision complex | ZSWAP |

# Syntax

| Fortran | CALL SSWAP $\mid$ DSWAP $\mid$ CSWAP $\mid$ ZSWAP $(n, x, incx, y, incy)$ |
| :--- | :--- |
| C and C++ | sswap $\mid$ dswap $\mid$ cswap $\mid$ zswap $(n, x, incx, y, incy)$; |

# On Entry:

$n$ is the number of elements in vectors $x$ and $y$.

Specified as: a fullword integer; $n \geq 0$.

$x$ is the vector $x$ of length $n$. Specified as: a one-dimensional array of (at least) length $1+(n-1) \lvert incx \rvert$, containing numbers of the data type indicated in Table 55.

$incx$ is the stride for vector $x$.

Specified as: a fullword integer. It can have any value.

$y$ is the vector $y$ of length $n$. Specified as: a one-dimensional array of (at least) length $1+(n-1) \lvert incy \rvert$, containing numbers of the data type indicated in Table 55.

$incy$ is the stride for vector $y$.

Specified as: a fullword integer. It can have any value.

# On Return:

$x$ is the vector $x$ of length $n$, containing the elements that were swapped from vector $y$. Returned as: a one-dimensional array, containing numbers of the data type indicated in Table 55.

$y$ is the vector $y$ of length $n$, containing the elements that were swapped from vector $x$. Returned as: a one-dimensional array, containing numbers of the data type indicated in Table 55.

# Notes

+   1. If you specify the same vector for $x$ and $y$, then $incx$ and $incy$ must be equal; otherwise, results are unpredictable.
+   2. If you specify different vectors for $x$ and $y$, they must have no common elements; otherwise, results are unpredictable. See “Concepts” on page 55.