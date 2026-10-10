13. Error 1015 is recoverable or \(n_{\text{aux2}} = 0\) and \(n_{\text{aux2}}\) is too small \(\left\right.\) that is, less than the minimum required value. Return code 7 is returned for \(n_{\text{aux2}}\) if error 1015 is recoverable.

# Example 1

This example finds the solution of the linear system \(\boldsymbol{Ax} = \boldsymbol{b}\) for the sparse matrix \(\boldsymbol{A}\), which is stored by rows in arrays \(\boldsymbol{AR}\), \(\boldsymbol{IA}\), and \(\boldsymbol{JA}\). The system is solved using the Bi-CGSTAB algorithm. The iteration is stopped when the norm of the residual is less than the given threshold specified in RPARM(1). The algorithm is allowed to perform 20 iterations. The process converges after 9 iterations. Matrix \(\boldsymbol{A}\) is:

![](bbox=[0.35, 0.24, 0.72, 0.37])

# Call Statement and Input:

```
```
                  STOR  INIT     N      AR      JA      IA     B     X      IPARM    RPARM    AUX1     NAUX1     AUX2     NAUX2
                   |      |       |      |       |       |     |     |      |        |        |        |        |        |
CALL DSRIS( 'G' , 'I' , 9 , AR , JA , IA , B , X , IPARM , RPARM , AUX1 , 98 , AUX2 , 63 )
AR   = (2.0, 2.0, -1.0, 1.0, 2.0, 1.0, 2.0, -1.0, 1.0, 2.0, -1.0,
        1.0, 2.0, -1.0, 1.0, 2.0, -1.0, 1.0, 2.0, -1.0, 1.0, 2.0, 2.0)
JA   = (1, 2, 3, 2, 3, 1, 4, 5, 4, 5, 6, 5, 6, 7, 7, 8, 7, 8,
         9, 8, 9)
IA   = (1, 2, 4, 6, 9, 12, 15, 18, 21, 23)
B    = (2.0, 1.0, 3.0, 2.0, 2.0, 2.0, 2.0, 2.0, 3.0)
X    = (0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0)
IPARM(1) = 20
IPARM(2) = 4
IPARM(3) = 0
IPARM(4) = 1
IPARM(5) = 10
RPARM(1) = 1.0 D-7
RPARM(3) = 1.0
```

```

# Output:

```
```
X          = (1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0)
IPARM(6)  = 9
RPARM(2)  = 0.29D-16
```

```

# Example 2

This example finds the solution of the linear system \(\boldsymbol{Ax} = \boldsymbol{b}\) for the same sparse matrix \(\boldsymbol{A}\) used in Example 1. It also uses the same right-hand side in \(\boldsymbol{b}\) and the same initial guesses in \(\boldsymbol{x}\). However, the system is solved using a different algorithm, conjugate gradient squared (CGS). Because INIT is S, the best performance is achieved. The iteration is stopped when the norm of the residual is less than the given threshold specified in RPARM(1). The algorithm is allowed to perform 20 iterations. The process converges after 9 iterations.