input matrix is assumed to be positive or negative definite. Vector \( x \) contains the results of the last iteration. The value \( i \) is identified in the computational error message.

+   For error 2108, return code 4 indicates that the matrix is not positive definite. AC is partially modified and does not represent the same matrix as on entry.

# Input-Argument Errors:

+   1. \( iopt \neq 0 \) or 1
+   2. \( m < 0 \)
+   3. \( lda < 1 \)
+   4. \( lda < m \)
+   5. \( nd < 0 \)
+   6. \( nd = 0 \) and \( m > 0 \)
+   7. \( \vert \lambda(i) \vert > m-1 \) for \( i = 1, nd \)
+   8. \( IPARM(1) < 0 \)
+   9. \( IPARM(2) \neq 0, 1, \) or \( 2 \)
+   10. \( IPARM(3) \neq 0, 10, \) or \( -10 \)
+   11. \( RPARM(1) < 0 \)
+   12. \( RPARM(2) < 0 \)
+   13. Error 2015 is recoverable or \(\text{naux1}\#0\), and \(\text{naux1}\) is too small—that is, less than the minimum required value. Return code 5 is returned if error 2015 is recoverable.
+   14. \(\text{naux2}\) is too small—that is, less than the minimum required value. Return code 5 is returned if error 2015 is recoverable.

# Example 1

This example finds the solution of the linear system \( A x = b \) for sparse matrix \( A \), which is stored in compressed-diagonal storage mode in arrays AD and LA. The system is solved using the two-term conjugate gradient method. In this example, IOPT = 0.. Matrix A is:

![](bbox=[0.35, 0.57, 0.76, 0.69])

# Call Statement and Input:

```
IOPT M ND AD LDA LA B X IPARM RPARM AUX1 AUX1 AUX2 NADX2
| | | | | | | | | | | |
CALL DSDCG( 0 , 9 , 3 , AD , 9 , LA , B , X , IPARM , RPARM , AUX1 , 283 , AUX2 , 0 )

IPARM(1) = 20
IPARM(2) = 0
IPARM(3) = 0
RPARM(1) = 1.0-7
```

![](bbox=[0.27, 0.88, 0.5, 0.96])