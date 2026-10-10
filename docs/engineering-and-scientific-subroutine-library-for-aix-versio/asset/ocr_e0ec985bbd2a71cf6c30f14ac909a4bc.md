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

# Example 2

This example shows how to factor the 9 by 9 general sparse matrix $A$ from Example 1, solve the system $Ax = b$ with three right-hand sides, and compute the determinant of $A$. The default values for pivot processing are used for IPARM. Input matrix $A$ is stored in profile-in skyline storage mode. Output matrix $A$ is in $LU$ factored form with $U^{-1}$ on the diagonal, and is stored in diagonal-out skyline storage mode. It is the same as output matrix $A$ in Example 1.

Call Statement and Input:

```
       N AU NU IDU AL NL IDL IPARM RPARAM AUX NAUX BX LDBX MBX
       |  |  |  |  |  |  |     |     |    |    |  |     |  |
CALL DGKFS( 9, AU, 33, IDU, AL, 35, IDL, IPARM, RPARAM, AUX, 57, BX, 12, 3 )
```