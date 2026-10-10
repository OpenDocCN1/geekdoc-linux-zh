
## Input-Argument Error Messages

- Element (_ ) in (ARG NO. _) must be greater than or equal to zero and less than or equal to 1.
- Element (_ ) in (ARG NO. _) must be greater than the preceding element.
- Element (_ ) in (ARG NO. _) must be greater than or equal to 1 and less than or equal to n.
- Element (_ ) in (ARG NO. _) must be -1 or 1.
- Element (_ ) in (ARG NO. _) must be nonzero.
- Element (_ ) in (ARG NO. _) must be 0, 1, 2, 10, or 11.
- Element (_ ) in (ARG NO. _) must be 0, 1, 2, 10, 11, 100, 102, or 110.
- Element (_ ) in (ARG NO. _) must be 0.
- Element (_ ) in (ARG NO. _) must be 1.
- Element (_ ) in (ARG NO. _) must be 0, 1, 2, 10, 11, 100, 101, 102, 110, or 111.
- Element (_ ) in (ARG NO. _) must be 1, 2, 3, or 4.
- Element (_ ) in (ARG NO. _) must be 1, 2, 3, 4, or 5.

RTN_NAME : 2538-2071 The number of eigenvalues (ARG NO. _) must be less than or equal to the order of the matrix (ARG NO. _).

RTN_NAME : 2538-2072 The work area (ARG NO. _) does not contain a valid vector seed. The routine must be called with a nonzero value of ISEED (ARG NO. _).

RTN_NAME : 2538-2073 (ARG NO. _) must be a double precision whole number greater than or equal to 1.0 and less than 2147483647.0.

RTN_NAME : 2538-2074 Performance can be improved by using a larger work array. For best performance, specify the number of elements (ARG NO. _ ) in the work array to be greater than or equal to (_ ).

RTN_NAME : 2538-2075 The data type parameter (ARG NO. _) must be 'S', 'D', 'C', or 'Z'.

RTN_NAME : 2538-2076 (ARG NO. _) must be greater than or equal to (_ ) and smaller than (_ ).

RTN_NAME : 2538-2077 The matrix is singular. Column (_ ) is empty in the matrix specified by (ARG NO. _ ), (ARG NO. _ ), and (ARG NO. _ ).

RTN_NAME : 2538-2078 The matrix is singular. Row (_ ) is empty in the matrix specified by (ARG NO. _ ), (ARG NO. _ ), and (ARG NO. _ ).

RTN_NAME : 2538-2079 The matrix, specified by (ARG NO. _ ), (ARG NO. _ ), and (ARG NO. _ ), contains at least one duplicate column index in row (_ ).

RTN_NAME : 2538-2080 Element (_ ) in (ARG NO. _ ) must be greater than or equal to (_ ) and less than or equal to (_ ).
or
Element (_ ) in (ARG NO. _) must be greater than or equal to (_ ) and less than or equal to (ARG NO. _ ).
or
Element (_ ) in (ARG NO. _) must be greater than or equal to element (_ ) and less than or equal to (_ ).
or
Element (_ ) in (ARG NO. _) must be zero or must be greater than or equal to (_ ).

RTN_NAME : 2538-2081 Element ( ) in (ARG NO. ) must be less than or equal to ( ).

RTN_NAME : 2538-2082 Element ( ) in (ARG NO. ) may cause incorrect or misleading results. A nonzero number with absolute value less than or equal to 1 is recommended.

RTN_NAME : 2538-2083 The pivot tolerance (element ( ) in (ARG NO. ) ) may cause incorrect or misleading results. A number greater than or equal to 0 and less than or equal to 1 is recommended.

RTN_NAME : 2538-2084 The dimension (ARG NO. ) of the array (ARG NO. ) must be greater than or equal to ( ).

RTN_NAME : 2538-2085 The number of steps after which the generalized minimum residual method is restarted, element ( ) in (ARG NO. ), must be greater than 0.

RTN_NAME : 2538-2086 The acceleration parameter, element ( ) in (ARG NO. ), must be greater than 0 when using the SSOR preconditioner.

RTN_NAME : 2538-2087 STOR (ARG NO. ), which specifies the storage variation used to represent the input sparse matrix, must be ‘G’, ‘L’, or ‘U’.

RTN_NAME : 2538-2088 INIT (ARG NO. ), which specifies the type of computation to be performed, must be ‘I’ or ‘S’.

RTN_NAME : 2538-2089 Element ( ) in (ARG NO. ) must be greater than or equal to ( ).
or
Element ( ) in (ARG NO. ) must be greater than or equal to element ( _ ).

RTN_NAME : 2538-2090 For level ( ), the number of grid points for dimension ( ) must be an odd number greater than 1.

RTN_NAME : 2538-2091 Since the mesh spacing (ARG NO. ) here is not constant, the second order prolongation method must be used. That is, element ( ) of (ARG NO. ) must be ( ).
or
Element ( ) in (ARG NO. ) may cause incorrect or misleading results. A positive number less than or equal to 1 is recommended.

RTN_NAME : 2538-2092 The index into (ARG NO. ) is out of range. This index is element (_,_ ) of (ARG NO. ).

RTN_NAME : 2538-2093 The index into (ARG NO. ) is out of range. This index is element (_,_ ) of (ARG NO. ).

RTN_NAME : 2538-2094 For dimension ( ) on level ( ), the mesh spacing must be changed to a positive value.

RTN_NAME : 2538-2095 Excess space in (ARG NO. ) has been decreased and may be inadequate. To avoid this, specify the coarse level matrix as the final item in this argument.

RTN_NAME : 2538-2096 For level ( ), the matrix type, solver, and preconditioner are incompatible.

RTN_NAME : 2538-2097 The solver requested for level ( ) requires a square matrix. Elements ( _ ) and ( _ ) in (ARG NO. ) must be equal.

RTN_NAME : 2538-2098 Element ( _ ) of (ARG NO. ) must be greater than or equal to ( ).

RTN_NAME : 2538-2099 End of input argument error reporting. For more information, refer to Engineering and Scientific Subroutine Library Guide and Reference (SA22-7904).

Note: There are more input-argument error messages listed in "Input-Argument Error Messages(2200-2299)" on page 184.

## Computational Error Messages(2100-2199)

RTN_NAME : 2538-2100 The computed index of a vector is out of the range (_) to (_).

RTN_NAME : 2538-2101 Eigenvalue (_) failed to converge after (_) iterations.

RTN_NAME : 2538-2102 Eigenvector (_) failed to converge after (_) iterations.

RTN_NAME : 2538-2103 The matrix (ARG NO. _) is singular. Zero diagonal element (_) has been detected.

RTN_NAME : 2538-2104 The matrix (ARG NO. _) is not positive definite. The last diagonal element with nonpositive value is (_).

RTN_NAME : 2538-2105 Factorization failed due to near zero pivot number (_).

RTN_NAME : 2538-2106 Vector boundary misalignment detected in ESSL scalar library.

RTN_NAME : 2538-2107 Singular value (_) failed to converge after (_) iterations.

RTN_NAME : 2538-2108 The matrix specified by (ARG NO. _) and (ARG NO. _) is not definite because the diagonal is not of constant sign.

RTN_NAME : 2538-2109 The matrix specified by (ARG NO. _) and (ARG NO. _) is not definite and the iterative process is stopped at iteration number (_).

RTN_NAME : 2538-2110 The maximum allowed number of iterations, element number (_) of (ARG NO. _), were performed but the iterative process did not converge to a solution according to the stopping procedure.

RTN_NAME : 2538-2111 The factorization matrix (ARG NO. _) is not consistent with the sparse matrix specified by (ARG NO. _) and (ARG NO. _).

RTN_NAME : 2538-2112 The incomplete factorization of the sparse matrix specified by (ARG NO. _) and (ARG NO. _) is not stable.

RTN_NAME : 2538-2113 Unexpected nonzero vector mask detected in ESSL scalar routine. Contact your IBM Service Representative.

RTN_NAME : 2538-2114 Eigenvalue (_) failed to converge after (_) iterations.

RTN_NAME : 2538-2115 The matrix (ARG NO. _) is not positive definite. The leading minor of order (_) has a nonpositive determinant.

RTN_NAME : 2538-2116 The matrix specified by (ARG NO. _) and (ARG NO. _) is singular.

RTN_NAME : 2538-2117 The pivot element in column (_) is smaller than the first element in (ARG NO. _).

RTN_NAME : 2538-2118 The pivot element in row (_) is smaller than the first element in (ARG NO. _).

RTN_NAME : 2538-2119 The storage space, specified by (ARG NO. _), is insufficient.

RTN_NAME : 2538-2120 The matrix is singular. The last row processed in the matrix was row (_).

RTN_NAME : 2538-2121 The matrix is singular. The last column processed was column (_).

RTN_NAME : 2538-2122 The factorization failed. No pivot element was found in the active submatrix.

RTN_NAME : 2538-2123 Performance can be improved by specifying a larger value for (ARG NO. _). (_) compressions were performed.

RTN_NAME : 2538-2124 The data contained in AUXI (ARG NO. _) was computed for a different algorithm.

RTN_NAME : 2538-2126 The pivot value at row (_) is not acceptable based on pivot criteria ((ARG NO. _) and (ARG NO. _)). No fixup was applicable to this pivot. The matrix (ARG NO. _) may be singular or not definite.

RTN_NAME : 2538-2127 The pivot value at row (_) was replaced with element (_) in (ARG NO. _). The matrix (ARG NO. _) may be singular or not definite.

RTN_NAME : 2538-2128 Internal ESSL error, contact your IBM service representative.

RTN_NAME : 2538-2129 The matrix specified by (ARG NO. _), (ARG NO. _), and (ARG NO. _) is not definite because the diagonal is not of constant sign or some diagonal element is zero.

RTN_NAME : 2538-2130 The incomplete factorization of the sparse matrix specified by (ARG NO. _), (ARG NO. _), and (ARG NO. _) is not stable.

RTN_NAME : 2538-2131 The matrix specified by (ARG NO. _), (ARG NO. _), and (ARG NO. _) is singular.

RTN_NAME : 2538-2132 Element (_) in (ARG NO. _) indicates that factorization was done on a previous call. The data passed is not the result of a prior valid factorization.

RTN_NAME : 2538-2133 An error occurred on level (_) in the user-supplied subroutine specified by (ARG NO. _).

RTN_NAME : 2538-2134 The data contained in (ARG NO. _) is not consistent with the sparse matrix specified by (ARG NO. _), (ARG NO. _), and (ARG NO. _).

RTN_NAME : 2538-2135 For level (_), loss of orthogonality occurred in a minimum residual solver because the input matrix (element (._) of (ARG NO. _)) is inappropriate. Choose one of the other non-symmetric solvers.

RTN_NAME : 2538-2136 For level (_), the main diagonal element for row (_) of a matrix is 0.

RTN_NAME : 2538-2145 The input matrix (ARG NO. _) is singular. The first diagonal element found to be exactly zero was in column (_).

RTN_NAME : 2538-2146 The input matrix (ARG NO. _) is singular. The first diagonal element found to be exactly zero was in column (_).

RTN_NAME : 2538-2147 The matrix (ARG NO. _) is singular. Zero diagonal element (_) has been detected.

RTN_NAME : 2538-2148 The matrix (ARG NO. _) is not positive definite. The leading minor of order (_) has a nonpositive determinant.

RTN_NAME : 2538-2149 Factorization failed due to near zero pivot number (_).

RTN_NAME : 2538-2150 The inverse of matrix (ARG NO. _) could not be computed. The first diagonal element of the factored matrix found to be exactly zero was in column (_).

RTN_NAME : 2538-2151 The inverse of matrix (ARG NO. _) could not be computed. The first diagonal element of the factored matrix found to be exactly zero was in column (_).

RTN_NAME : 2538-2199 End of computational error reporting. For more information, refer to Engineering and Scientific Subroutine Library Guide and Reference (SA22-7904).
