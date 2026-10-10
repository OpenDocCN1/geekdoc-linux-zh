
## DGKFS

The determinant can be computed with any of the factorization computations.
With a full factorization, you get the determinant for the whole matrix. With a
partial factorization, you get the determinant for only that part of the matrix
factored in this computation.

The system $A x = b$ or $A^{T}x = b$, having multiple right-hand sides, is solved for $x$, using the transformed matrix $A$ produced by this call or a subsequent call to this subroutine.

See references [11], [14], [27], [49], and [73]. If $n$ is 0, no computation is performed.
If $mbx$ is 0, no solve is performed.

## Error Conditions

### Resource Errors

- Error 1015 is unrecoverable, $naux = 0$, and unable to allocate work area.
- Unable to allocate internal work area.

### Computational Errors

- 1. If a pivot occurs in region $i$ for $i = 1, 5$ and $IPARM(10+i) = 1$, the pivot value is replaced with $RPARM(10+i)$, an attention message is issued, and processing continues.
- 2. Unacceptable pivot values occurred in the factorization of matrix $A$.
    - One or more diagonal elements of $U$ contains unacceptable pivots and no valid fixup is applicable. The row number $i$ of the first unacceptable pivot element is identified in the computational error message.
    - The return code is set to 2.
    - $i$ can be determined at run time by use of the ESSL error-handling facilities.
    - To obtain this information, you must use ERRSET to change the number of allowable errors for error code 2126 in the ESSL error option table; otherwise, the default value causes your program to terminate when this error occurs. For details, see “What Can You Do about ESSL Computational Errors?” on page 47.

### Input-Argument Errors

- 1. $n < 0$
- 2. $nu < 0$
- 3. $IDU(n+1) > nu+1$
- 4. $IDU(i+1) \le IDU(i)$ for $i = 1, n$
- 5. $IDU(i+1) > IDU(i)+i$ and $IPARM(4) = 0$ for $i = 1, n$
- 6. $IDU(i) > IDU(i-1)+i$ and $IPARM(4) = 1$ for $i = 2, n$
- 7. $nl < 0$
- 8. $IDL(n+1) > nl+1$
- 9. $IDL(i+1) \le IDL(i)$ for $i = 1, n$
- 10. $IDL(i+1) > IDL(i)+i$ and $IPARM(4) = 0$ for $i = 1, n$
- 11. $IDL(i) > IDL(i-1)+i$ and $IPARM(4) = 1$ for $i = 2, n$
- 12. $IPARM(1) \neq 0$ or 1
- 13. $IPARM(2) \neq 0, 1, 2, 10, 11, 100, 102, \text{or } 110$
- 14. $IPARM(3) < 0$
- 15. $IPARM(3) > n$
- 16. $IPARM(3) > 0$ and $IPARM(2) \neq 1$ or 11
- 17. $IPARM(4), IPARM(5) \neq 0$ or 1
- 18. $IPARM(2) = 0, 1, 10, 11, 100, \text{or } 110$ and:
    - $IPARM(10) \neq 0$ or 1
    - $IPARM(11), IPARM(12) \neq -1, 0, \text{or } 1$
    - $IPARM(13) \neq -1$ or 1
- 19. $IPARM(14), IPARM(15) \neq -1, 0, \text{or } 1$
- 20. $RPARAM(10) < 0.0$
- 21. $RPARAM(10+i) = 0.0$ and $IPARM(10+i) = 1$ for $i = 1, 5$
- 22. $IPARM(2) = 0, 2, 10, 100, 102, \text{or } 110$ and:
    - $ldbx \leq 0$ and $mbx \neq 0$ and $n \neq 0$
    - $ldbx < 0$ and $mbx = 0$
    - $ldbx < n$ and $mbx \neq 0$
    - $mbx < 0$
- 23. Error 2015 is recoverable or $naux \neq 0$, and $naux$ is too small---that is, less than the minimum required value. Return code 1 is returned if error 2015 is recoverable.

## Example 1

This example shows how to factor a 9 by 9 general sparse matrix $A$ and solve the system $A x=b$ with three right-hand sides. The default values are used for IPARM and RPARAM. Input matrix $A$, shown here, is stored in diagonal-out skyline storage mode. Matrix $A$ is:

![](img/5b0f44f3be6048723819b26aed7f6f03_636_0.png)

Output matrix $A$, shown here, is in $LU$ factored form with $U^{-1}$ on the diagonal, and is stored in diagonal-out skyline storage mode. Matrix $B$ is:

![](img/5b0f44f3be6048723819b26aed7f6f03_636_1.png)

### Call Statement and Input:

```
       N   AU   NU  IDU   AL   NL   IDL  IPARM  RPARAM  AUX  NAUX  BX  LDBX MBX
       |    |    |   |    |   |    |     |      |     |   |   |   |    |
CALL DGKFS( 9 , AU, 33, IDU, AL, 35, IDL, IPARM, RPARAM, AUX, 57 , BX , 12 , 3 )

AU   = (2.0, 4.0, 2.0, 6.0, 4.0, 2.0, 6.0, 4.0, 2.0, 4.0, 6.0,
         4.0, 2.0, 6.0, 2.0, 16.0, 10.0, 8.0, 10.0, 4.0, 6.0, 4.0, 2.0, 2.0)
IDU  = (1, 2, 4, 7, 10, 14, 17, 22, 26, 34)
AL   = (0.0, 0.0, 2.0, 0.0, 4.0, 2.0, 8.0, 6.0, 6.0, 2.0, 0.0,
         2.0, 0.0, 8.0, 6.0, 4.0, 2.0, 0.0, 6.0, 4.0, 2.0, 0.0,
         8.0, 6.0, 4.0, 2.0, 0.0, 0.0, 10.0, 10.0, 6.0, 8.0, 6.0,
         4.0, 2.0)
IDL  = (1, 2, 4, 7, 2, 11, 13, 18, 22, 27, 36)
IPARM = (0, ., ., ., ., ., ., ., ., ., ., ., ., ., ., .)
       = (. , . , . , . , . , . , . , . , . , . , . , . , . , . , . , .)
RPARAM =(not relevant)
```

```
BX = 

|  6.00 | 12.00 | 18.00 |
| 16.00 | 32.00 | 48.00 |
| 26.00 | 52.00 | 78.00 |
| 36.00 | 72.00 | 108.00 |
| 48.00 | 40.00 | 60.00 |
| 48.00 | 96.00 | 144.00 |
| 34.00 | 68.00 | 102.00 |
| 38.00 | 76.00 | 114.00 |
| 66.00 | 132.00 | 198.00 |
|   .    |   .    |   .    |
|   .    |   .    |   .    |
```

Output:

```
AU       = ( 0.5, 0.5, 2.0, 0.5, 2.0, 2.0, 0.5, 2.0, 2.0, 0.5,
2.0,          2.0, 2.0, 0.5, 2.0, 2.0, 0.5, 2.0, 2.0, 2.0, 2.0, 0.5,
2.0, 2.0, 2.0, 0.5, 2.0, 2.0, 2.0, 2.0, 2.0, 2.0, 2.0, 2.0 )
IDU      =(same as input)
AL       = ( 0.0, 0.0, 1.0, 0.0, 1.0, 1.0, 0.0, 1.0, 1.0, 1.0, 0.0,
1.0, 0.0, 1.0, 0.0, 1.0, 1.0, 0.0, 1.0, 1.0, 1.0, 0.0,
1.0, 1.0, 1.0, 1.0, 0.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0 )
IDL      =(same as input)
IPARM    = ( 0, ., ., ., ., ., ., ., ., ., ., ., ., 9, ., ., ., ., ., .,
. , . , . , . , . , . , . , 0 , 0 , 0 , . , 9 )
RPARAM   = ( ., ., ., ., ., ., ., ., ., ., ., ., ., ., ., ., ., .,
. , 8.0, ., ., ., ., ., ., ., ., ., ., ., . )
```

```
BX = 

| 1.00 | 2.00 | 3.00 |
| 1.00 | 2.00 | 3.00 |
| 1.00 | 2.00 | 3.00 |
| 1.00 | 2.00 | 3.00 |
| 1.00 | 2.00 | 3.00 |
| 1.00 | 2.00 | 3.00 |
| 1.00 | 2.00 | 3.00 |
| 1.00 | 2.00 | 3.00 |
| 1.00 | 2.00 | 3.00 |
|   .  |   .   |   .   |
|   .  |   .   |   .   |
|   .  |   .   |   .   |
```

## Example 2

This example shows how to factor the 9 by 9 general sparse matrix $A$ from Example 1, solve the system $Ax = b$ with three right-hand sides, and compute the determinant of $A$. The default values for pivot processing are used for IPARM. Input matrix $A$ is stored in profile-in skyline storage mode. Output matrix $A$ is in $LU$ factored form with $U^{-1}$ on the diagonal, and is stored in diagonal-out skyline storage mode. It is the same as output matrix $A$ in Example 1.

### Call Statement and Input:

```
       N AU NU IDU AL NL IDL IPARM RPARAM AUX NAUX BX LDBX MBX
       |  |  |  |  |  |  |     |     |    |    |  |     |  |
CALL DGKFS( 9, AU, 33, IDU, AL, 35, IDL, IPARM, RPARAM, AUX, 57, BX, 12, 3 )

AU = (2.0, 2.0, 4.0, 2.0, 4.0, 6.0, 2.0, 4.0, 6.0, 2.0, 4.0, 6.0, 4.0, 2.0, 4.0, 6.0, 2.0, 4.0, 4.0, 8.0, 8.0, 2.0, 4.0, 6.0, 8.0, 2.0, 4.0, 6.0, 4.0, 10.0, 8.0, 10.0, 16.0)
IDU = (1, 3, 6, 9, 13, 16, 21, 25, 33, 34)
AL = (0.0, 2.0, 0.0, 2.0, 4.0, 2.0, 4.0, 6.0, 0.0, 2.0, 0.0, 2.0, 4.0, 6.0, 8.0, 0.0, 2.0, 4.0, 6.0, 0.0, 2.0, 4.0, 6.0, 8.0, 0.0, 2.0, 4.0, 6.0, 8.0, 10.0, 8.0, 0.0)
IDL = (1, 3, 6, 10, 12, 17, 21, 26, 35, 36)
IPARM = (1, 110, 0, 1, 0, * * * * * * * * * * * * 0, * * * * * * * * * * * * 0, * * * * * * * * * * * *)
RPARAM = (not relevant)

BX = 
[ 10.00    20.00    30.00
  20.00    40.00    60.00
  28.00    56.00    84.00
  30.00    60.00    90.00
  40.00    80.00   120.00
  30.00    60.00    90.00
  44.00    88.00   132.00
  28.00    56.00    84.00
  60.00   120.00   180.00
  .        .         .
  .        .         .
  .        .         .
]
```

Output:

```
AU = (same as output AU in Example 1)
IDU = (same as output IDU in Example 1)
AL = (same as output AL in Example 1)
IDL = (same as output IDL in Example 1)
IPARM = (1, 110, 0, 1, 0, * * * * * * * * * * 0, * * * * * * * * * * * 0, * * * * * * * * * * * 0, 0, 0, 0, 9)
RPARM = ( * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * 8.0, 5.12, 2.0, * * * * * * * * * * )
BX = (same as output BX in Example 1)
```

## Example 3

This example shows how to factor a 9 by 9 negative-definite general sparse matrix A, solve the system Ax = b with three right-hand sides, and compute the determinant of A. (Default values for pivot processing are not used for IPARM because A is negative-definite.) Input matrix A, shown here, is stored in diagonal-out skyline storage mode:

```
[ -2.0   -2.0   -2.0    0.0    0.0    0.0    0.0    0.0    0.0
  -2.0   -4.0   -4.0   -2.0   -2.0    0.0    0.0    0.0   -2.0
  -2.0   -4.0   -6.0   -4.0   -4.0    0.0   -2.0    0.0   -4.0
  -2.0   -4.0   -6.0   -6.0   -6.0   -2.0   -4.0    0.0   -6.0
   0.0    0.0    0.0   -2.0   -4.0   -4.0   -4.0   -2.0   -4.0
   0.0   -2.0   -4.0   -6.0   -8.0   -6.0   -8.0   -4.0  -10.0
   0.0    0.0    0.0   -2.0   -4.0   -6.0   -8.0   -6.0   -8.0
   0.0    0.0    0.0   -2.0   -4.0   -6.0   -8.0   -8.0  -10.0
  -2.0   -4.0   -6.0   -6.0   -8.0  -10.0   -8.0   -8.0  -16.0
]
```

Output matrix A, shown here, is in LU factored form with $U^{-1}$ on the diagonal, and is stored in diagonal-out skyline storage mode. Matrix A is:
