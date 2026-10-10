# SPBF, DPBF, SPBCHF, and DPBCHF

# Notes

+   1. These subroutines can be used for tridiagonal matrices (*m* = 1); however, the tridiagonal subroutines, SPTF/DPTF and SPTS/DPPTS, are faster.
+   2. For SPBF and DPBF when *m* > 0, location APB(2, *n*) is sometimes set to 0.
+   3. For a description of how a positive definite symmetric band matrix is stored in lower-band-packed storage mode in an array, see "Positive Definite Symmetric Band Matrix" on page 83.

# Function

The positive definite symmetric band matrix *A*, stored in lower-band-packed storage mode, is factored using Gaussian elimination in SPBF and DPBF and Cholesky factorization in SPBCHF and DPBCHF. The transformed matrix *A* contains the results of the factorization in packed format. This factorization can then be used by SPBS, DPBS, SPBCHS, and DPBCHS, respectively, to solve the system of equations.

For performance reasons, divides are done in a way that reduces the effective exponent range for which DPBF works properly, when processing narrow band widths; therefore, you may want to scale your problem.

# Error Conditions

Resource Errors: Unable to allocate internal work area.

Computational Errors:

+   1. Matrix *A* is not positive definite (for SPBF and DPBF).
+   	* One or more elements of *D* contain values less than or equal to 0; all elements of *D* are checked. The index *i* of the last nonpositive element encountered is identified in the computational error message.
+   	* The return code is set to 1.
+   	* *i* can be determined at run time by use of the ESSL error-handling facilities. To obtain this information, you must use ERRSET to change the number of allowable errors for error code 2104 in the ESSL error option table; otherwise, the default value causes your program to terminate when this error occurs. For details, see Chapter 4, "Coding Your Program," on page 107.
+   2. Matrix *A* is not positive definite (for SPBCHF and DPBCHF).
+   	* The leading minor of order *i* has a nonpositive determinant. The order *i* is identified in the computational error message.
+   	* The return code is set to 1.
+   	* *i* can be determined at run time by use of the ESSL error-handling facilities. To obtain this information, you must use ERRSET to change the number of allowable errors for error code 2115 in the ESSL error option table; otherwise, the default value causes your program to terminate when this error occurs. For details, see Chapter 4, "Coding Your Program," on page 107.

Input-Argument Errors:

+   1. *lda* ≤ 0
+   2. *m* < 0
+   3. *m* ≥ *n*
+   4. *m* ≥ *lda*

# Example 1

This example shows a factorization of a real positive definite symmetric band matrix *A* of order 9, using Gaussian elimination, where on input, matrix *A* is: