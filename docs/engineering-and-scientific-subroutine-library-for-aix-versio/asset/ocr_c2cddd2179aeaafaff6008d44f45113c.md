ESSL Development
Department 85BA
Mail Station P963
2455 South Rd.
Poughkeepsie, N.Y. 12601-5400

e-mail: essl@us.ibm.com

Note: You should send us e-mail if you would like to be withdrawn from the ESSL mailing list.

When requesting to be placed on the mailing list or asking any questions, please provide the following information:

+   - Your name
+   - The name of your company
+   - Your mailing address
+   - Your Internet address
+   - Your phone number

# List of ESSL Subroutines

This section provides an overview of the subroutines in each of the areas of ESSL.

Appendix A, “Basic Linear Algebra Subprograms (BLAS),” on page 987 contains a list of Level 1, 2, and 3 Basic Linear Algebra Subprograms (BLAS) included in ESSL.

Appendix B, “LAPACK,” on page 989 contains a list of Linear Algebra Package (LAPACK) subroutines included in ESSL.

# Linear Algebra Subprograms

The linear algebra subprograms consist of:

+   - Vector-scalar linear algebra subprograms (Table 6)
+   - Sparse vector-scalar linear algebra subprograms (Table 7)
+   - Matrix-vector linear algebra subprograms (Table 8)
+   - Sparse matrix-vector linear algebra subprograms (Table 9)

Notes:

+   1. The term **subprograms** is used to be consistent with the Basic Linear Algebra Subprograms (BLAS), because many of these subprograms correspond to the BLAS.
+   2. Some of the linear algebra subprograms were designed in accordance with the Level 1 and Level 2 BLAS de facto standard. If these subprograms do not comply with the standard as approved, IBM will consider updating them to do so. If IBM updates these subprograms, the updates could require modifications of the calling application program.

# Vector-Scalar Linear Algebra Subprograms

The vector-scalar linear algebra subprograms include a subset of the standard set of Level 1 BLAS. For details on the BLAS, see reference [81]. The remainder of the vector-scalar linear algebra subprograms are commonly used computations provided for your applications. Both real and complex versions of the subprograms are provided.