# SNRM2, DNRM2, SCNRM2, and DZNRM2—Euclidean Length of a Vector with Scaling of Input to Avoid Destructive Underflow and Overflow

These subprograms compute the Euclidean length ($l_2$ norm) of vector $x$, with scaling of input to avoid destructive underflow and overflow.

**Table 50. Data Types**

| $\mathbf{x}$ | Result | Subprogram |
|---|---|---|
| Short-precision real | Short-precision real | SNRM2 |
| Long-precision real | Long-precision real | DNRM2 |
| Short-precision complex | Short-precision real | SCNRM2 |
| Long-precision complex | Long-precision real | DZNRM2 |

**Note:** If there is a possibility that your data will cause the computation to overflow or underflow, you should use these subroutines instead of SNORM2, DNORM2, CNORM2, and ZNORM2, because the intermediate computational results may exceed the maximum or minimum limits of the machine. “Notes” on page 233 explains how to estimate whether your data will cause an overflow or underflow.

# Syntax

|  |  |
|---|---|
| **Fortran** | SNRM2 \| DNRM2 \| SCNRM2 \| DZNRM2 $n, x, incx$ |
| **C and C++** | snrm2 \| dnrm2 \| scnrm2 \| dznrn2 $(n, x, incx)$; |

**On Entry:**

+   *   $n$ is the number of elements in vector $x$. Specified as: a fullword integer; $n \geq 0$.
+       *   $x$ is the vector $x$ of length $n$, whose Euclidean length is to be computed. Specified as: a one-dimensional array of (at least) length $1 + (n-1)|incx|$, containing numbers of the data type indicated in Table 50.
+       *   $incx$ is the stride for vector $x$. Specified as: a fullword integer. It can have any value.

**On Return:**
*Function value* is the Euclidean length ($l_2$ norm) of the vector $x$. Returned as: a number of the data type indicated in Table 50.

**Note**
Declare this function in your program as returning a value of the data type indicated in Table 50.

**Function**
The Euclidean length ($l_2$ norm) of vector $x$ is expressed as follows, with scaling of input to avoid destructive underflow and overflow: