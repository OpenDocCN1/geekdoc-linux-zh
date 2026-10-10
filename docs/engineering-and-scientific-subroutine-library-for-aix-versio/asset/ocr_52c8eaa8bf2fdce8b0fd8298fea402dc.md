# SGTNPF, DGTNPF CGTNPF, and ZGTNPF

On Return:

+   *   c is the vector *c*, containing part of the factorization of matrix *A* in positions 1 through *n* in an array, referred to as C. Returned as: a one-dimensional array of (at least) length *n*, containing numbers of the data type indicated in Table 119 on page 577.
+   *   d is the vector *d*, containing part of the factorization of matrix *A* in an array, referred to as D. Returned as: a one-dimensional array of (at least) length *n*, containing numbers of the data type indicated in Table 119 on page 577.
+   *   e is the vector *e*, containing part of the factorization of matrix *A* in positions 1 through *n* in an array, referred to as E. Returned as: a one-dimensional array of (at least) length *n*, containing numbers of the data type indicated in Table 119 on page 577. It has the same length as E on entry.

**Note** For a description of how tridiagonal matrices are stored, see “General Tridiagonal Matrix” on page 88.

# Function

The factorization of a diagonally-dominant tridiagonal matrix *A* is computed using Gaussian elimination. This factorization can then be used by SGTNPS, DGTNPS, CGTNPS, or ZGTNPS respectively, to solve the tridiagonal systems of linear equations. See reference [79].

No pivoting is done by these subroutines. Therefore, these subroutines should not be used when pivoting is necessary to maintain the numerical accuracy of the solution. Overflow may occur if small main diagonal elements are generated. Underflow or accuracy loss may occur if large main diagonal elements are generated.

For performance reasons, complex divides are done without scaling. Computing the inverse in this way restricts the range of numbers for which ZGTNPF works properly.

For performance reasons, divides are done in a way that reduces the effective exponent range for which DGTNPF and ZGTNPF work properly; therefore, you may want to scale your problem, such that the diagonal elements are close to 1.0 for DGTNPF and (1.0, 0.0) for ZGTNPF.

# Error Conditions

Computational Errors: None

Input-Argument Errors:

+   1. *n* < 0
+   2. *iopt* ≠ 0 or 1

# Example 1

This example shows a factorization of the tridiagonal matrix *A*, of order 4:

```
1.0 1.0 0.0 0.0
1.0 2.0 1.0 0.0
0.0 1.0 3.0 1.0
0.0 0.0 1.0 1.0
```

Call Statement and Input: