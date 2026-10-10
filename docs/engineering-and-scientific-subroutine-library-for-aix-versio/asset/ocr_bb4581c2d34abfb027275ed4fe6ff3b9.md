# SGBF and DGBF—General Band Matrix Factorization

These subroutines factor general band matrix *A*, stored in general-band storage mode, using Gaussian elimination. To solve the system of equations with one or more right-hand sides, follow the call to these subroutines with one or more calls to SGBS or DGBS, respectively.

Table 112. Data Types

| A | Subroutine |
| --- | --- |
| Short-precision real | SGBF |
| Long-precision real | DGBF |

> **Note:** The output from these factorization subroutines should be used only as input to the solve subroutines SGBS and DGBS, respectively.

# Syntax

| Fortran | CALL SGBF \| DGBF (*agb*, *lda*, *n*, *ml*, *mu*, *ipvt*) |
| C and C++ | *sgbf* \| *dgbf* (*agb*, *lda*, *n*, *ml*, *mu*, *ipvt*); |

**On Entry:**

+   *agb* is the general band matrix *A* of order *n*, stored in general-band storage mode, to be factored. It has an upper band width *mu* and a lower band width *ml*. Specified as: an *lda* by (at least) *n* array, containing numbers of the data type indicated in Table 112, where *lda* ≥ 2*ml*+*mu*+16.

+   *lda* is the leading dimension of the array specified for *agb*. Specified as: a fullword integer; *lda* > 0 and *lda* ≥ 2*ml*+*mu*+16.

+   *n* is the order of the matrix *A*. Specified as: a fullword integer; *n* > *ml* and *n* > *mu*.

+   *ml* is the lower band width *ml* of the matrix *A*. Specified as: a fullword integer; 0 ≤ *ml* < *n*.

+   *mu* is the upper band width *mu* of the matrix *A*. Specified as: a fullword integer; 0 ≤ *mu* < *n*.

+   *ipvt* See “On Return.”

**On Return:**

+   *agb* is the transformed matrix *A* of order *n*, containing the results of the factorization. See “Function” on page 558. Returned as: an *lda* by (at least) *n* array, containing numbers of the data type indicated in Table 112.

+   *ipvt* is the integer vector *ipvt* of length *n*, containing the pivot information necessary to construct matrix *L* from the information contained in the output array *agb*. Returned as: a one-dimensional array of (at least) length *n*, containing fullword integers.

# Notes

+   1. *ipvt* is not a permutation vector in the strict sense. It is used to record column interchanges in *L* due to partial pivoting and to improve performance.

+   2. The entire *lda* by *n* array specified for *agb* must remain unchanged between calls to the factorization and solve subroutines.