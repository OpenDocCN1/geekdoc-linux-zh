# SPPSV and DPPSV

*ap* is an array, referred to as *AP*, in which the transformed matrix *A* of order *n*, containing the results of the factorization, is stored in upper- or lower-packed storage mode.

Returned as: a one-dimensional array of (at least) length $n(n+1)/2$, containing numbers of the data type indicated in Table 98 on page 468. See “Function.”

*bx* is the general matrix *X*, containing the *nrhs* solutions to the system. The solutions, each of length *n*, reside in the columns of *X*.

Returned as: an *ldb* by (at least) *nrhs* array, containing numbers of the data type indicated in Table 98 on page 468.

*info* has the following meaning:

If *info* = 0, the subroutine completed successfully.

If *info* > 0, the factorization was unsuccessful. *B* is overwritten; that is, the original input is not preserved. *info* is set equal to the order *i* of the first minor encountered having a nonpositive determinant.

Specified as: a fullword integer; *info* ≥ 0.

# Notes

+   1.  These subroutines accept lowercase letters for the *uplo* argument.
+   2.  In your *C* program, argument *info* must be passed by reference.
+   3.  The matrices used in this computation must have no common elements; otherwise, results are unpredictable. See “Concepts” on page 55.
+   4.  For a description of how a positive definite symmetric matrix is stored in upper- or lower-packed storage mode in an array, see “Positive Definite or Negative Definite Symmetric Matrix” on page 69.
+   5.  On both input and output, matrices *A*, *B*, and *X* conform to LAPACK format.
+   6.  The way these subroutines handle computational errors differs from LAPACK. These subroutines use the *info* argument to provide information about the computational error, like LAPACK, but also provide an error message.

# Function

The system $\mathbf{AX} = \mathbf{B}$ is solved for $\mathbf{X}$, where $\mathbf{A}$ is a positive definite real symmetric matrix, and $\mathbf{X}$ and $\mathbf{B}$ are real general matrices.

The matrix $A$, stored in upper- or lower-packed storage mode, is factored using the Cholesky factorization method, where $A$ is expressed as $A = \mathbf{U}^{T}\mathbf{U}$ or $A = \mathbf{L}\mathbf{L}^{T}$, where:

+   *   $\mathbf{U}$ is an upper triangular matrix.
+   *   $\mathbf{L}$ is a lower triangular matrix.

If $n$ is 0, no computation is performed and the subroutine returns after doing some parameter checking. If $n > 0$ and *nrhs* is 0, no solutions are computed and the subroutine returns after factoring the matrix.

See references [8], [38], and [40].

# Error Conditions

**Resource Errors:** Unable to allocate internal work area.

**Computational Errors:**