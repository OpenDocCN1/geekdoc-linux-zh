# SPOTRS, DPOTRS, CPOTRS, ZPOTRS, SPOSM, DPOSM, CPOSM, ZPOSM, SPPTRS, and DPPTRS

A = (same as output A in “Example 1” on page 482)

BX = $\begin{bmatrix} 9.0 & 45.0 \\ 17.0 & 89.0 \\ 24.0 & 131.0 \\ 30.0 & 170.0 \\ 35.0 & 205.0 \\ 39.0 & 235.0 \\ 42.0 & 259.0 \\ 44.0 & 276.0 \\ 45.0 & 285.0 \end{bmatrix}$

Output:

BX = $\begin{bmatrix} 1.0 & 1.0 \\ 1.0 & 2.0 \\ 1.0 & 3.0 \\ 1.0 & 4.0 \\ 1.0 & 5.0 \\ 1.0 & 6.0 \\ 1.0 & 7.0 \\ 1.0 & 8.0 \\ 1.0 & 9.0 \end{bmatrix}$

INFO = 0

# Example 2

This example shows how to solve the system $AX = B$ for two right-hand sides, where matrix $A$ is the input matrix factored in “Example 2” on page 483 for SPOTRF and SPOF.

**Call Statement and Input:**

UPLO N NRHS A LDA BX LDB INFO
```
        |   |   |   |   |   |   |   |
CALL SPOTRS( 'U', 9, 2, A, 9, BX, 9, INFO )
OR
UPLO A LDA N BX LDB NRHS
   |   |   |   |   |   |   |
CALL SPOSM( 'U', A, 9, 9, BX, 9, 2 )
```

A = (same as output A in “Example 2” on page 483)

BX = $\begin{bmatrix} 9.0 & 45.0 \\ 17.0 & 89.0 \\ 24.0 & 131.0 \\ 30.0 & 170.0 \\ 35.0 & 205.0 \\ 39.0 & 235.0 \\ 44.0 & 276.0 \\ 45.0 & 285.0 \end{bmatrix}$

Output:

BX = $\begin{bmatrix} 1.0 & 1.0 \\ 1.0 & 2.0 \\ 1.0 & 3.0 \\ 1.0 & 4.0 \\ 1.0 & 5.0 \\ 1.0 & 6.0 \end{bmatrix}$