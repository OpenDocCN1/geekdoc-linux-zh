# SNORM2, DNORM2, CNORM2, and ZNORM2—Euclidean Length of a Vector with No Scaling of Input

These subprograms compute the euclidean length ($l_2$ norm) of vector $x$ with no scaling of input.

Table 51. Data Types

| x | Result | Subprogram |
| --- | --- | --- |
| Short-precision real | Short-precision real | SNORM2 |
| Long-precision real | Long-precision real | DNORM2 |
| Short-precision complex | Short-precision real | CNORM2 |
| Long-precision complex | Long-precision real | ZNORM2 |

# Syntax

| Fortran | SNORM2 | DNORM2 | CNORM2 | ZNORM2 $(n, x, incx)$ |
| --- | --- | --- | --- | --- |
| C and C++ | snorm2 | dnorm2 | cnorm2 | znorm2 $(n, x, incx)$; |

On Entry:

$n$
is the number of elements in vector $x$. Specified as: a fullword integer; $n \ge 0$.

$x$
is the vector $x$ of length $n$, whose euclidean length is to be computed.
Specified as: a one-dimensional array of (at least) length $1+(n-1) \cdot incx$, containing numbers of the data type indicated in Table 51.

$incx$
is the stride for vector $x$.
Specified as: a fullword integer. It can have any value.

On Return:

$Function\ value$
is the euclidean length ($l_2$ norm) of the vector $x$. Returned as: a number of the data type indicated in Table 51.

# Notes

+   1. This subroutine does not underflow or overflow if the values of the elements in vector $x$ conform to the following conditions. If these conditions are violated, overflow or destructive underflow may occur:
+      - For short-precision numbers:
+        Any valid short-precision number.
+      - For long-precision numbers:
+        $|x_i| = 0$ or $0.10010E-145 < |x_i| < 0.13408E+155$ for $i = 1, n$
+   2. Declare this function in your program as returning a value of the data type indicated in Table 51.

# Function

The euclidean length ($l_2$ norm) of vector $x$ is expressed as follows with no scaling of input: