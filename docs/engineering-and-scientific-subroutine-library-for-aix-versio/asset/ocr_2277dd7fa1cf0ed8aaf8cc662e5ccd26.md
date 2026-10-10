# SGTS and DGTS—General Tridiagonal Matrix Solve

These subroutines solve a tridiagonal system of linear equations using the factorization of tridiagonal matrix A, stored in tridiagonal storage mode, produced by SGTF or DGTF, respectively.

# Table 117. Data Types

| c, d, e, f, b, x | Subroutine |
| :--------------- | :--------- |
| Short-precision real | SGTS |
| Long-precision real | DGTS |

Note: The input to these solve subroutines must be the output from the factorization subroutines SGTF and DGTF, respectively.

# Syntax

| Fortran | CALL SGTS \| DGTS (n, c, d, e, f, ipvt, bx) |
| :-- | :--- |
| C and C++ | sgts \| dgts (n, c, d, e, f, ipvt, bx); |

# On Entry:

+   - **n** is the order n of tridiagonal matrix A. Specified as: a fullword integer; n ≥ 0.

+   - **c** is the vector c, containing part of the factorization of matrix A from SGTF or DGTF, respectively, in an array, referred to as C. Specified as: a one-dimensional array of (at least) length n, containing numbers of the data type indicated in Table 117.

+   - **d** is the vector d, containing part of the factorization of matrix A from SGTF or DGTF, respectively, in an array, referred to as D. Specified as: a one-dimensional array of (at least) length n, containing numbers of the data type indicated in Table 117.

+   - **e** is the vector e, containing part of the factorization of matrix A from SGTF or DGTF, respectively, in an array, referred to as E. Specified as: a one-dimensional array of (at least) length n, containing numbers of the data type indicated in Table 117.

+   - **f** is the vector f, containing part of the factorization of matrix A from SGTF or DGTF, respectively, in an array, referred to as F. Specified as: a one-dimensional array of (at least) length n, containing numbers of the data type indicated in Table 117.

+   - **ipvt** is the integer vector ipvt of length n, containing the pivot information, produced by a preceding call to SGTF and DGTF, respectively. Specified as: a one-dimensional array of (at least) length n, containing fullword integers.

+   - **bx** is the vector b of length n, containing the right-hand side of the system in the first n positions in an array, referred to as Bx. Specified as: a one-dimensional array of (at least) length n+1, containing numbers of the data type indicated in Table 117. For details on specifying the length, see “Notes” on page 573.

# On Return:

+   - **bx** is the solution vector x (at least) of length n, containing the solution of the tridiagonal system in the first n positions in an array, referred to as Bx.