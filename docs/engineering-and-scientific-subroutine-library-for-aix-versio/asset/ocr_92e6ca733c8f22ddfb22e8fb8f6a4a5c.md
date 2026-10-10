# SGESVF and DGESVF

+   7. $m < 0$
+   8. $n < 0$
+   9. Error 2015 is recoverable or `naux=0`, and `naux` is too small—that is, less than the minimum required value. Return code 2 is returned if error 2015 is recoverable.

# Example 1

This example shows how to find only the singular values, *s*, of a real long-precision general matrix *A*, where:

+   * *M* is greater than *N*.
+   * *NAUX* is greater than or equal to *N*+max(*M*,*N*) = 7.
+   * *LDB* has been set to 1 to avoid a Fortran error message.
+   * *DUMMY* is a placeholder for argument *b*, which is not used in the computation.
+   * The singular values are returned in *S*.
+   * On output, matrix *A* is overwritten; that is, the original input is not preserved.

# Call Statement and Input:

```
IOP    A   LDA     B    LDB  NB   S   M    N   AUX NAUX
     |     |    |     |    |    |   |    |   |    |    |
CALL DGESVF( 0  ,  A  , 4  , DUMMY  , 1  , 0  , S  , 4  , 3  , AUX  , 7  )
```

![](bbox=[0.28, 0.38, 0.49, 0.44])

# Output:

S = (25.462, 1.291, 0.000)

# Example 2

This example computes the singular values, *s*, of a real long-precision general matrix *A* and the matrix *V*, where:

+   * *M* is equal to *N*.
+   * *NAUX* is greater than or equal to 2*N*+max(*M*,*N*) = 9.
+   * *LDB* has been set to 1 to avoid a Fortran error message.
+   * *DUMMY* is a placeholder for argument *b*, which is not used in the computation.
+   * The singular values are returned in *S*.
+   * The matrix *V* is returned in *A*.

# Call Statement and Input:

```
IOP    A   LDA     B    LDB  NB   S   M    N   AUX NAUX
     |     |    |     |    |    |   |    |   |    |    |
CALL DGESVF( 1  ,  A  , 3  , DUMMY  , 1  , 0  , S  , 3  , 3  , AUX  , 9  )
```

![](bbox=[0.28, 0.72, 0.45, 0.77])

# Output:

![](bbox=[0.28, 0.81, 0.55, 0.86])

S = (4.922, 2.724, 0.597)