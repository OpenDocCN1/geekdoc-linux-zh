# SGETRS, DGETRS, CGETRS, and ZGETRS

+   7.  On both input and output, matrices A and B conform to LAPACK format.

# Function

One of the following systems of equations is solved for multiple right-hand sides:

+   1. AX = B
+   2. A T X = B
+   3. A H X = B (only for CGETRS and ZGETRS)

where A, B, and X are general matrices. These subroutines uses the results of the factorization of matrix A, produced by a preceding call to SGETF R, DGETF R, CGETF R or ZGETF R, respectively. For details on the factorization, see "SGETRF, DGETF R, CGETF R and ZGETRF—General Matrix Factorization" on page 444.

If n = 0 or nrhs = 0, no computation is performed and the subroutine returns after doing some parameter checking. See references [8], [38], and [64].

# Error Conditions

Computational Errors: None

> Note: If the factorization performed by SGETF R, DGETF R, CGETF R or ZGETF R failed because a pivot element is zero, the results returned by this subroutine are unpredictable, and there may be a divide-by-zero program exception message.

Input-Argument Errors:

+   1. transa ≠ 'N', 'T, or 'C'
+   2. n < 0
+   3. nrhs < 0
+   4. n > lda
+   5. lda ≤ 0
+   6. n > ldb
+   7. ldb ≤ 0

# Example 1

This example shows how to solve the system AX = B, where matrix A is the same matrix factored in the "Example 1" on page 445 for DGETFR.

Call Statement and Input:

```
TRANSAX NRHS A LDA IPVIX BX LDB INFO
CALL DGETRS('N', 9, 5, A, 9, IPV1, BX, 9, INFO)
```

IPVT = (9, 9, 9, 9, 9, 9, 9, 9, 9)
A = (same as output A in "Example 1" on page 445)

93.0 186.0 279.0 372.0 465.0
84.4 168.8 253.2 337.6 422.0
76.6 153.2 229.8 306.4 383.0
70.0 140.0 210.0 280.0 350.0
65.0 130.0 195.0 260.0 325.0
62.0 124.0 186.0 248.0 310.0
61.4 122.8 184.2 245.6 307.0
63.6 127.2 190.8 254.4 318.0
69.0 138.0 207.0 276.0 345.0

Output: