# ## SWLEV, DWLEV, CWLEV, and ZWLEV—Wien er-Levinson Filter Coefficients

These subroutines compute the coefficients of an $n$-point Wiener-Levinson filter, using vector $\mathbf{x}$, the trace for which the filter is to be designed, and vector $\mathbf{u}$, the right-hand side of the system, chosen to remove reverberations or sharpen the wavelet. The result is returned in vector $\mathbf{y}$.

Table 154. Data Types

| $\mathbf{x}$, $\mathbf{u}$, $\mathbf{y}$ | aux | Subroutine |
| :--- | :--- | :--- |
| Short-precision real | Long-precision real | SWLEV |
| Long-precision real | Long-precision real | DWLEV |
| Short-precision complex | Long-precision complex | CWLEV |
| Long-precision complex | Long-precision complex | ZWLEV |

# ### Syntax

| Fortran | `CALL SWLEV \| DWLEV \| CWLEV \| ZWLEV ( (x, incx, u, incu, y, incy, n, aux, naux)` |
| :--- | :--- |
| C and C++ | `swlev \| dwlev \| cwlev \| zwlev ( x, incx, u, incu, y, incy, n, aux, naux);` |

# ### On Entry:

$\mathbf{x}$ is the vector $\mathbf{x}$ of length $n$, containing the trace data for which the filter is to be designed.

For SWLEV and DWLEV, $\mathbf{x}$ represents the first row (or the first column) of a positive definite or negative definite symmetric Toeplitz matrix, which is the autocorrelation matrix for which the filter is designed.

For CWLEV and ZWLEV, $\mathbf{x}$ represents the first row of a positive definite or negative definite complex Hermitian Toeplitz matrix, which is the autocorrelation matrix for which the filter is designed.

Specified as: a one-dimensional array of (at least) length $1+(n-1) \times |incx|$ , containing numbers of the data type indicated in Table 154.

$incx$ is the stride for vector $\mathbf{x}$.

Specified as: a fullword integer; $incx > 0$.

$\mathbf{u}$ is the vector $\mathbf{u}$ of length $n$, containing the right-hand side of the system to be solved.

Specified as: a one-dimensional array of (at least) length $1+(n-1) \times |incu|$ , containing numbers of the data type indicated in Table 154.

$incu$ is the stride for vector $\mathbf{u}$.

Specified as: a fullword integer. It can have any value.

$\mathbf{y}$ See “On Return” on page 872.

$incy$ is the stride for vector $\mathbf{y}$.

Specified as: a fullword integer; $incy > 0$ or $incy < 0$.

$n$ is the number of elements in vectors $\mathbf{x}$, $\mathbf{u}$, and $\mathbf{y}$.

Specified as: a fullword integer; $n \geq 0$.

$aux$ has the following meaning: