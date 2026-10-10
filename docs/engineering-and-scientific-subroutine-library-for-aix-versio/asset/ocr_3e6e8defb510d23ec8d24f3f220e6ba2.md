# SPOTRI, DPOTRI, CPOTRI, ZPOTRI, SPOICD, DPOICD, SPICD, and DPICD

+   5.  **SPPICD** and **DPPICD** in some cases utilize algorithms based on recursive packed storage format. (See references [54], [68], and [69]).
+   6.  The way `*_POTRI` subroutines handle computational errors differs from LAPACK. These subroutines use the `info` argument to provide information about the computational error, like LAPACK, but also provide an error message.
+   7.  On both input and output, matrix $A$ conforms to LAPACK format.
+   8.  For a description of how a positive definite symmetric matrix is stored in lower-packed storage mode in an array, see “Symmetric Matrix” on page 64. For a description of how a positive definite symmetric matrix is stored in upper or lower storage mode, see “Positive Definite or Negative Definite Symmetric Matrix” on page 69.
+   9.  You have the option of having the minimum required value for `naux` dynamically returned to your program. For details, see “Using Auxiliary Storage in ESSTL” on page 32.

# Function

These subroutines perform the following function:

# **SPOTRI, DPOTRI, CPOTRI, and ZPOTRI**

Find the inverse of positive definite matrix $A$.

# **SPOICD, DPOICD, SPICD, and DPICD**

Find the inverse, the reciprocal of the condition number, and the determinant of positive definite symmetric matrix $A$ using Cholesky factorization, where:

+   *   $A^{-1}$ is the inverse of matrix $A$, where $AA^{-1} = A^{-1}A = I$, and $I$ is the identity matrix.
+   *   $1/(\|A\|_3 \|A^{-1}\|_3)$ is the reciprocal of the condition number, where $\|A\|_3$ is the one-norm of matrix $A$.
+   *   $|A|$ is the determinant of matrix $A$, where $|A|$ is expressed as:

$det_1(10^{det_1})$

The *iopt* argument is used to determine the combination of output items produced by this subroutine: the inverse, the reciprocal of the condition number, and the determinant.

If $n$ is 0, no computation is performed. See references [38], [40], and [46].

# Error Conditions

+   **Resource Errors:**
+   *   Unable to allocate internal work area.
+   *   Error 2015 is unrecoverable, `naux = 0`, and unable to allocate work area.
+   
+   **Computational Errors:**
+   **For SPOTRI, DPOTRI, CPOTRI, and ZPOTRI:**
+   
+   The inverse of matrix $A$ could not be computed.
+   *   One or more of the diagonal elements of the factored matrix $A$ are zero.
+   
+   The first diagonal element that is found to be exactly zero is identified in