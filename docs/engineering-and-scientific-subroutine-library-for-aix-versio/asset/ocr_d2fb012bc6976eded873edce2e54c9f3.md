# SGEMMS, DGEMMS, CGEMMS, and ZGEMMS

# Notes

+   1. There are two instances when these subroutines use the direct method (`_GEMUL`), rather than using Strassen's algorithm:
+   	* When either or both of the input matrices are small
+   	* For CGEMMS and ZGEMMS, when input matrices *A* and *B* overlap
+   
+   		In these instances when the direct method is used, the subroutine does not use auxiliary storage, and you can specify *naux* = 0.

+   2. For CGEMMS and ZGEMMS, one of the input matrices, *A* or *B*, is rearranged during the computation and restored to its original form on return. Keep this in mind when diagnosing an abnormal termination.

+   3. All subroutines accept lowercase letters for the *transa* and *transb* arguments.

+   4. Matrix *C* must have no common elements with matrices *A* or *B*; otherwise, results are unpredictable. See "Concepts" on page 55.

+   5. You have the option of having the minimum required value for *naux* dynamically returned to your program. For details, see "Using Auxiliary Storage in ESSLL" on page 32.

# Function

The matrix multiplications performed by these subroutines are functionally equivalent to those performed by SGEMUL, DGEMUL, CGEMUL, and ZGEMUL. For details on the computations performed, see "Function" on page 379.

SGEMMS, DGEMMS, CGEMMS, and ZGEMMS use Winograd's variation of the Strassen's algorithm with minor changes for tuning purposes. (See pages 45 and 46 in reference [13].) The subroutines compute matrix multiplication for both real and complex matrices of large sizes. Complex matrix multiplication uses a special technique, using three real matrix multiplications and five real matrix additions. Each of these three resulting matrix multiplications then uses Strassen's algorithm.

**Strassen's Algorithm:** The steps of Strassen's algorithm can be repeated up to four times by these subroutines, with each step reducing the dimensions of the matrix by a factor of two. The number of steps used by this subroutine depends on the size of the input matrices. Each step reduces the number of operations by about 10% from the normal matrix multiplication. On the other hand, if the matrix is small, a normal matrix multiplication is performed without using the Strassen's algorithm, and no improvement is gained. For details about small matrices, see "Notes."

**Complex Matrix Multiplication:** The complex multiplication is performed by forming the real and imaginary parts of the input matrices. These subroutines uses three real matrix multiplications and five real matrix additions, instead of the normal four real matrix multiplications and two real matrix additions. Using only three real matrix multiplications allows the subroutine to achieve up to a 25% reduction in matrix operations, which can result in a significant savings in computing time for large matrices.

**Accuracy Considerations:** Strassen's method is not stable for certain row or column scalings of the input matrices *A* and *B*. Therefore, for matrices *A* and *B* with divergent exponent values Strassen's method may give inaccurate results. For these cases, you should use the `_GEMUL` or `_GEMM` subroutines.

# Special Usage

The equivalence rules, defined for matrix multiplication of *A* and *B* in "Special Usage" on page 380, also apply to these subroutines. You should use the