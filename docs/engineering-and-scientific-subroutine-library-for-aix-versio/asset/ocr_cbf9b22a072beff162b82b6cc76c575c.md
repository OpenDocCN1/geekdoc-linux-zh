# SDOT, DDOT, CDOTU, ZDOTU, CDOTC, and ZDOTC—Dot Product of Two Vectors

SDOT, DDOT, CDOTU, and ZDOTU compute the dot product of vectors x and y:

$x \bullet y$

CDOTC and ZDOTC compute the dot product of the complex conjugate of vector x with vector y:

$\bar{x} \bullet y$

Table 47. Data Types
| x, y, Result | Subprogram |
| :--- | :--- |
| Short-precision real | SDOT |
| Long-precision real | DDOT |
| Short-precision complex | CDOTU and CDOTC |
| Long-precision complex | ZDOTU and ZDOTC |

# Syntax

| | |
| :--- | :--- |
| Fortran | `SDOT | DDOT | CDOTU | ZDOTU | CDOTC | ZDOTC (n, x, incx, y, incy)` |
| C and C++ | `sdot | ddot | cdotu | zdotu | cdotc | zdotc (n, x, incx, y, incy);` |

+   On Entry:
+   * n is the number of elements in vectors x and y.
+   Specified as: a fullword integer; n ≥ 0.
+   * x is the vector x of length n. Specified as: a one-dimensional array of (at least) length 1+(n−1)|incx|, containing numbers of the data type indicated in Table 47.
+   * incx is the stride for vector x.
+   Specified as: a fullword integer. It can have any value.
+   * y is the vector y of length n. Specified as: a one-dimensional array of (at least) length 1+(n−1)|incy|, containing numbers of the data type indicated in Table 47.
+   * incy is the stride for vector y.
+   Specified as: a fullword integer. It can have any value.

+   On Return:
+   * Function value is the result of the dot product computation. Returned as: a number of the data type indicated in Table 47.

+   Note
+   Declare this function in your program as returning a value of the data type indicated in Table 47.