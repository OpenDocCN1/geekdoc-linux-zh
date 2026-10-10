# Notes

+   The array data specified for input argument *ap* for these subroutines must be the same as the corresponding output argument for SPPE/SPPFCD and DPPF/DPPF/DPPFCD, respectively.
+   The scalar data specified for input argument *n* for these subroutines must be the same as that specified for SPPE/SPPFCD and DPPF/DPPF/DPPFCD, respectively.
+   When you call these subroutines after calling SPPE or DPPE, the value of input argument *iopt* must be as follows:

| SPPE/DPPE Input iopt | SPSS/DPPS Input iopt |
|---|---|
| 0 or 10 | 0 |
| 1 or 11 | 1 |

+   When you call these subroutines after calling SPFCD or DPPFCD, the value of input argument *iopt* must be 0.
+   When you call these subroutines after calling DPPPE, the value of input argument *iopt* must be 1.
+   In the input array specified for *ap*, the first *n*( *n* +1)/2 elements are matrix elements. The additional *n* locations, required in the array when *iopt* = 0, are used for working storage by this subroutine and should not be altered between calls to the factorization and solve subroutines.
+   The vectors and matrices used in this computation must have no common elements; otherwise, results are unpredictable. See "Concepts" on page 55.
+   For a description of how a positive definite symmetric matrix is stored in lower-packed storage mode in an array, see "Symmetric Matrix" on page 64.

# Function

The system *Ax* = *b* is solved for *x*, where *A* is a positive definite symmetric matrix, stored in lower-packed storage mode in array *AP*, and *x* and *b* are vectors. These subroutines use the results of the factorization of matrix *A*, produced by a preceding call to SPPE/SPPFCD or DPPE/DPPF/DPPFCD, respectively.

If *n* is 0, no computation is performed. See references [38] and [40].

# Error Conditions

Computational Errors: None

> Note: If a call to SPPE, DPPE, SPFCD, DPPFCD, or DPPF resulted in a nonpositive definite matrix, error 2104 or 2115, SPSS or DPPS results may be unpredictable or numerically unstable.

Input-Argument Errors:
1. *n* < 0
2. *iOpt* ≠ 0 or 1

# Example 1

This example shows how to solve the system *Ax* = *b*, where matrix *A* is the same matrix factored in the "Example 7" on page 486 for SPPE and DPPE.

# Call Statement and Input:

```
AP
N
BX
IOPT
CALL SPSS ( AP , 9 , BX , 0 )
```