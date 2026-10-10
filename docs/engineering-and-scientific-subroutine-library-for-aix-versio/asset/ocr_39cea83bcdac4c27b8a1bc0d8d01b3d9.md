SGETRI, DGETRI, CGETRI, ZGETRI, SGEICD, and DGEICD

# Notes

+   1. In your C program, arguments `rcond` and `info` must be passed by reference.
+   2. The input scalar arguments for SGETRI, DGETRI, CGETRI, and ZGETRI must be set to the same values as the corresponding input arguments in the previous call to SGETRF, DGETRF, CGETRF, and ZGETRF, respectively.
+      If `iopt` = 4, the input scalar arguments for SGEICD and DGEICD must be set to the same values as the corresponding input arguments in the previous call to SGEF /SGEFC or DGEF /DGECFD /DGEFF, respectively.
+   3. You have the option of having the value for `nuxx` dynamically returned to your program. For details, see “Using Auxiliary Storage in ESSL” on page 32.
+   4. The way _GETRI subroutines handle computational errors differs from LAPACK. These subroutines use the `info` argument to provide information about the computational error, like LAPACK, but also provide an error message.
+   5. On both input and output, matrix $A$ conforms to LAPACK format.
+   6. For best performance, specify `lwork` = 0.

# Function

**For subroutines SGETRI, DGETRI, CGETRI, and ZGETRI:**

The inverse of general square matrix $A$ is computed.

**For subroutines SGEICD and DGEICD:**

The inverse, the reciprocal of the condition number, and the determinant of a general square matrix $A$ are computed using partial pivoting to preserve accuracy, where:
- $A^{-1}$ is the inverse of matrix $A$, where $AA^{-1} = A^{-1}A = I$, and $I$ is the identity matrix.
- $1/(\lVert A\rVert_1\lVert A^{-1}\rVert_1)$ is the reciprocal of the condition number, where $\lVert A\rVert_1$ is the one-norm of matrix $A$.
- $\lvert A\rvert$ is the determinant of matrix $A$, where $\lvert A\rvert$ is expressed as:

$det_1(\lvert 10^{det_2}\rvert)$

The `iopt` argument is used to determine the combination of output items produced by this subroutine: the inverse, the reciprocal of the condition number, and the determinant.

If $n = 0$, no computation is performed. See references [38], [40], and [46].

# Error Conditions

+   **Resource Errors:**
+   1. Unable to allocate internal work area.
+   2. If `iopt` = 0, 1, 2, or 3, then error 2015 is unrecoverable, `nuxx` = 0, and unable to allocate work area.

+   **Computational Errors:** Matrix $A$ is singular or nearly singular.
+   
+   **For SGETRI, DGETRI, CGETRI, and ZGETRI:**
+   - The index $i$ of the first pivot element having a value equal to zero is identified in the computational error message.