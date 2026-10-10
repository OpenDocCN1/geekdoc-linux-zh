+   2. *lda* < 1
+   3. *lda* < *m*
+   4. *nz* < 0
+   5. *nz* = 0 and *m* > 0
+   6. IPARM(1) < 0
+   7. IPARM(2) ≠ 0, 1, or 2
+   8. IPARM(3) ≠ 0, 10, or −10
+   9. RPARM(1) < 0
+   10. RPARM(2) < 0

+   11. Error 2015 is recoverable or *nauxl*\*0, and *naux1* is too small—that is, less than the minimum required value. Return code 5 is returned if error 2015 is recoverable.

+   12. *naux2* is too small—that is, less than the minimum required value. Return code 5 is returned if error 2015 is recoverable.

# Example 1

This example finds the solution of the linear system *Ax* = *b* for the sparse matrix *A*, which is stored in compressed-matrix storage mode in arrays AC and KA. The system is solved using the conjugate gradient method. Matrix *A* is:

```
```
			[ 2.0  0.0  0.0  -1.0  0.0  0.0  0.0  0.0  0.0 ]
			[ 0.0  2.0 -1.0  0.0  0.0  0.0  0.0  0.0  0.0 ]
			[ 0.0 -1.0  2.0  0.0  0.0  0.0  0.0  0.0  0.0 ]
			[ -1.0 0.0  0.0  2.0 -1.0  0.0  0.0  0.0  0.0 ]
			[ 0.0  0.0  0.0 -1.0  2.0 -1.0  0.0  0.0  0.0 ]
			[ 0.0  0.0  0.0  0.0 -1.0  2.0 -1.0  0.0  0.0 ]
			[ 0.0  0.0  0.0  0.0  0.0 -1.0  2.0 -1.0  0.0 ]
			[ 0.0  0.0  0.0  0.0  0.0  0.0 -1.0  2.0 -1.0 ]
			[ 0.0  0.0  0.0  0.0  0.0  0.0  0.0 -1.0  2.0 ]
```
```

**Note**: For input matrix KA, ( . ) indicates any value between 1 and 9.

# Call Statement and Input:

```
```
			CALL DSMCG ( 9 , 3 , AC, KA, 9 , B , X, IPARM, RPARM, AUX1, 27 , AUX2, 0 )
```
```

```
```
IPARM(1)  =  20
IPARM(2)  =  0
IPARM(3)  =  0
RPARM(1)  =  1.0-7
```
```

```
```
AC  =  [ 2.0  -1.0  0.0
         2.0  -1.0  0.0
         -1.0 2.0  0.0
         +1.0 2.0 -1.0
         -1.0 2.0 -1.0
         -1.0 2.0 -1.0
         -1.0 2.0 -1.0
         -1.0 2.0  0.0 ]
```
```

```
```
KA  =  [ 1  4  .
         2  3  .
         2  3  4
         1  4  5
         4  5  6
         5  6  7 ]
```
```