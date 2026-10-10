# # DGKFS—General Sparse Matrix or Its Transpose Factorization, Determinant, and Solve Using Skyline Storage Mode

This subroutine can perform either or both of the following functions for general sparse matrix A, stored in skyline storage mode, and for vectors x and b:

+   • Factor A and, optionally, compute the determinant of A.
+   • Solve the system $Ax = b$ or $A^{T}x = b$ using the results of the factorization of matrix A, produced on this call or a preceding call to this subroutine.

You also have the choice of using profile-in or diagonal-out skyline storage mode for A on input or output.

Note: The input to the solve performed by this subroutine must be the output from the factorization performed by this subroutine.

# ## Syntax

| Fortran | CALL DGKFS (n, au, nu, iau, al, nl, idl, iparm, rparm, aux, naux, bx, ldx, mbx) |
| :------ | :--------------------------------------------------------------------- |
| C and C++ | dgkfs (n, au, nu, iau, al, nl, idl, iparm, rparm, aux, naux, bx, ldx, mbx); |

# ## On Entry:

n is the order of general sparse matrix A. Specified as: a fullword integer; $n \geq 0$.

au is the array, referred to as AU, containing one of three forms of the upper triangular part of general sparse matrix A, depending on the type of computation performed, where:

+   • If you are doing a **factor and solve** or a **factor only**, and if IPARM(3) = 0, then AU contains the unfactored upper triangle of general sparse matrix A.
+   • If you are doing a **factor only**, and if IPARM(3) > 0, then AU contains the partially factored upper triangle of general sparse matrix A. The first IPARM(3) columns in the upper triangle of A are already factored. The remaining columns are factored in this computation.
+   • If you are doing a **solve only**, then AU contains the factored upper triangle of general sparse matrix A, produced by a preceding call to this subroutine.

In each case:

If IPARM(4) = 0, diagonal-out skyline storage mode is used for A.

If IPARM(4) = 1, profile-in skyline storage mode is used for A.

Specified as: a one-dimensional array of (at least) length nu, containing long-precision real numbers.

nu is the length of array AU.

Specified as: a fullword integer; $nu = 0$ and $nu \geq (IDU(n+1)-1)$.

idu is the array, referred to as IDU, containing the relative positions of the diagonal elements of matrix A (in one of its three forms) in array AU.

Specified as: a one-dimensional array of (at least) length n+1, containing fullword integers.