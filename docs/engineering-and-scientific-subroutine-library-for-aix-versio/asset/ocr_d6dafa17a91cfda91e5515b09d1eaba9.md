+   2. The array data specified for input arguments *agb* and *ipvt* for these subroutines must be the same as the corresponding output arguments for SGBF and DGBF, respectively.
+   3. The entire *lda* by *n* array specified for *agb* must remain unchanged between calls to the factorization and solve subroutines.
+   4. The vectors and matrices used in this computation must have no common elements; otherwise, results are unpredictable. See “Concepts” on page 55.
+   5. This subroutine can be used for tridiagonal matrices (*ml* = *mu* = 1); however, the tridiagonal subroutines, SGTG/DGTG and SGTSS/DGTSS, are faster.
+   6. For a description of how a general band matrix is stored in general-band storage mode in an array, see “General Band Matrix” on page 75.

# Function

The real system *Ax* = *b* is solved for *x*, where *A* is a real general band matrix, stored in general-band storage mode, and *x* and *b* are vectors. These subroutines use the results of the factorization of matrix *A*, produced by a preceding call to SGBF or DGBF, respectively. The transformed matrix *A*, used by this computation, consists of the upper triangular matrix *U* and the multipliers necessary to construct *L* using *ipvt*, as defined in “Function” on page 558. See reference [40].

# Error Conditions

Computational Errors:

**Note:** If the factorization performed by SGBF or DGBF failed due to a singular matrix argument, the results returned by this subroutine are unpredictable, and there may be a divide-by-zero program exception message.

**Input-Argument Errors:**

+   1. *lda* ≤ 0
+   2. *ml* < 0
+   3. *ml* ≥ *n*
+   4. *mu* < 0
+   5. *mu* ≥ *n*
+   6. *lda* < 2*ml* + *mu* + 16

# Example

This example shows how to solve the system *Ax* = *b*, where general band matrix *A* is the same matrix factored in “Example” on page 558 for SGBF and DGBF. The input for AGB and IPVT in this example is the same as the output for that example.

**Call Statement and Input:**

```
          AGB       LDA       N       ML       MU       IPVT       BX
          |         |         |       |        |        |        |
CALL SGGS(AGB , 23 , 9 , 2 , 3 , IPVT , BX )

IPVT   = ( 2, -65534, -131070, -196606, -262142, -327678, -327678,
           -327680, -327680 )
BX     = ( 4.0000, 5.0000, 9.0000, 10.0000, 11.0000, 12.0000,
           12.0000, 12.0000, 33.0000 )
AGB    = ( same as output AGB in
           “Example” on page 558 )
```

**Output:**

```
BX     = ( 1.0000, 1.0000, 1.0000, 1.0000, 1.0000, 1.0000, 1.0000,
           0.9999, 1.0001 )
```