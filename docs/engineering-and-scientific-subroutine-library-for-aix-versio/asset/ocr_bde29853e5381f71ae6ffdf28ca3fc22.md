# SVEA, DVEA, CVEA, and ZVEA—Add a Vector X to a Vector Y and Store in a Vector Z

These subprograms perform the following computation, using vectors *x*, *y*, and *z*:
*\*z+x+y\**

# Table 56. Data Types

Table 56. Data Types
| x, y, z | Subprogram |
| Short-precision real | SVEA |
| Long-precision real | DVEA |
| Short-precision complex | CVEA |
| Long-precision complex | ZVEA |

# Syntax

Syntax
| Fortran | CALL SVEA \| DVEA \| CVEA \| ZVEA (n, x, incx, y, incy, z, incz) |
| C and C++ | svea \| dwea \| cwea \| zwwe (n, x, incx, y, incy, z, incz); |

# On Entry:

*n* is the number of elements in vectors *x*, *y*, and *z*.
Specified as: a fullword integer; *n* ≥ 0.

*x* is the vector *x* of length *n*. Specified as: a one-dimensional array of (at least) length 1+(n-1)|*incx*|, containing numbers of the data type indicated in Table 56.

*incx* is the stride for vector *x*.
Specified as: a fullword integer. It can have any value.

*y* is the vector *y* of length *n*. Specified as: a one-dimensional array of (at least) length 1+(n-1)|*incy*|, containing numbers of the data type indicated in Table 56.

*incy* is the stride for vector *y*.
Specified as: a fullword integer. It can have any value.

*z* See “On Return.”

*incz* is the stride for vector *z*.
Specified as: a fullword integer. It can have any value.

# On Return:

*z* is the vector *z* of length *n*, containing the result of the computation.
Returned as: a one-dimensional array of (at least) length 1+(n-1)|*incz*|, containing numbers of the data type indicated in Table 56.

# Notes

+   1. If you specify the same vector for *x* and *z*, then *incx* and *incz* must be equal; otherwise, results are unpredictable. The same is true for *y* and *z*.
+   2. If you specify different vectors for *x* and *z*, they must have no common elements; otherwise, results are unpredictable. The same is true for *y* and *z*. See “Concepts” on page 55.