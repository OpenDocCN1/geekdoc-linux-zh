
allowable errors for error code 2126 in the ESSL error option table; otherwise, the default value causes your program to terminate when this error occurs. For details, see “What Can You Do about ESSL Computational Errors?” on page 47.

## Input-Argument Errors:

- 1. *n* < 0
- 2. *na* < 0
- 3. IDIAG(*i+1*) ≤ IDIAG(*i*) for *i* = 1, *n*
- 4. IDIAG(*i+1*) > IDIAG(*i*) and IPARM(4) = 0 for *i* = 1, *n*
- 5. IDIAG(*i*) > IDIAG(*i−1*)+*i* and IPARM(4) = 1 for *i* = 2, *n*
- 6. IPARM(1) ≠ 0 or 1
- 7. IPARM(2) ≠ 0, 1, 2, 10, 11, 100, 101, 102, 110, or 111
- 8. IPARM(3) < 0
- 9. IPARM(3) > *n*
- 10. IPARM(3) > 0 and IPARM(2) ≠ 1, 11, 101, or 111
- 11. IPARM(4), IPARM(5) ≠ 0 or 1
- 12. IPARM(2) = 0, 1, 10, or 11 and:
    - IPARM(10) ≠ 0 or 1
    - IPARM(11), IPARM(12) ≠ −1, 0, or 1
    - IPARM(13) ≠ −1 or 1
    - IPARM(14), IPARM(15) ≠ −1, 0, or 1
    - RPARM(10) < 0.0
    - RPARM(10+*i*) = 0.0 and IPARM(10+*i*) = 1 for *i* = 1, 5
- 13. IPARM(2) = 100, 101, 110, or 111 and:
    - IPARM(10) ≠ 0 or 1
    - IPARM(11), IPARM(12), IPARM(13) ≠ −1 or 1
    - IPARM(14), IPARM(15) ≠ −1, 0, or 1
    - RPARM(10) < 0.0
    - RPARM(10+*i*) ≤ 0.0 and IPARM(10+*i*) = 1 for *i* = 1, 5
- 14. IPARM(2) = 0, 2, 10, 100, 102, or 110 and:
    - *ldb* < 0 and *mb* ≠ 0 and *n* ≠ 0
    - *ldb* < 0 and *mb* = 0
    - *ldb* < *n* and *mb* ≠ 0
    - *mb* < 0
- 15. Error 2015 is recoverable or *nax* ≠ 0, and *nax* is too small—that is, less than the minimum required value. Return code 1 is returned if error 2015 is recoverable.

## Example 1

This example shows how to factor a 9 by 9 symmetric sparse matrix *A* and solve the system *Ax = b* with three right-hand sides. It uses Gaussian elimination. The default values are used for IPARM and RPARM. Input matrix *A*, shown here, is stored in diagonal-out skyline storage mode. Matrix *A* is:

![](img/5b0f44f3be6048723819b26aed7f6f03_652_0.png)

### DSKFS

Output matrix *A*, shown here, is in $LDL^{T}$ factored form with $D^{-1}$ on the diagonal, and is stored in diagonal-out skyline storage mode. Matrix *A* is:

| 1.0 | 1.0 | 1.0 | 1.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 |
|---|---|---|---|---|---|---|---|---|
| 1.0 | 1.0 | 1.0 | 1.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 |
| 1.0 | 1.0 | 1.0 | 1.0 | 0.0 | 0.0 | 0.0 | 1.0 | 0.0 |
| 1.0 | 1.0 | 1.0 | 1.0 | 0.0 | 0.0 | 0.0 | 1.0 | 0.0 |
| 0.0 | 1.0 | 1.0 | 1.0 | 0.0 | 0.0 | 0.0 | 1.0 | 0.0 |
| 0.0 | 1.0 | 1.0 | 1.0 | 0.0 | 0.0 | 0.0 | 1.0 | 0.0 |
| 0.0 | 0.0 | 0.0 | 0.0 | 1.0 | 1.0 | 1.0 | 1.0 | 1.0 |
| 0.0 | 1.0 | 1.0 | 1.0 | 1.0 | 1.0 | 1.0 | 1.0 | 1.0 |
| 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 1.0 | 1.0 | 1.0 | 1.0 |

### Call Statement and Input:

```
N    A    NA IDIAG IPARM  RPARM  AUX AUXX BX  LDBX MBX
   |    |     |     |       |
CALL DSKFS( 9, A, 33, IDIAG, IPARM, RPARM, AUX, 39, BX, 12, 3 )
```

```
A   = (1.0, 2.0, 1.0, 3.0, 2.0, 1.0, 4.0, 3.0, 2.0, 1.0, 4.0,
     3.0, 2.0, 1.0, 5.0, 4.0, 3.0, 2.0, 1.0, 3.0, 2.0, 1.0,
     7.0, 3.0, 5.0, 4.0, 3.0, 2.0, 1.0, 4.0, 3.0, 2.0, 1.0)
```

```
IDIAG = (1, 2, 4, 7, 11, 15, 20, 23, 30, 34)
IPARM = (0, ., ., ., ., ., ., ., ., ., ., ., ., .,
      ., ., ., ., ., ., ., ., ., ., .)
```

```
RPARM =(not relevant)
```

```
BX  = [ 4.00   8.00  12.00
        10.00  20.00  30.00
        15.00  30.00  45.00
        19.00  38.00  57.00
        19.00  38.00  57.00
        23.00  46.00  69.00
        11.00  22.00  33.00
        28.00  56.00  84.00
        10.00  20.00  30.00
        ...    ...    ...
```

### Output:

```
A   = (1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0,
      1.0,
           1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0,
           1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0)
```

```
IDIAG =(same as input)
IPARM = (0, ., ., ., ., ., ., ., ., ., ., ., ., ., ., ., ., ., ., ., ., .,
         ., 8, ., ., ., ., ., 0, 0, 0, 0, 0, 9)
RPARM = ( ., ., ., ., ., ., ., ., ., ., ., ., ., ., ., ., ., ., .,
         ., 7.0, ., ., ., ., ., ., ., ., ., ., .)
```

```
BX  = [ 1.00   2.00   3.00
        1.00   2.00   3.00
        1.00   2.00   3.00
        1.00   2.00   3.00
        1.00   2.00   3.00
        1.00   2.00   3.00
        1.00   2.00   3.00
        1.00   2.00   3.00
```

![](img/5b0f44f3be6048723819b26aed7f6f03_654_0.png)

## Example 2

This example shows how to factor the 9 by 9 symmetric sparse matrix $A$ from Example 1, solve the system $Ax = b$ with three right-hand sides, and compute the determinant of $A$. It uses Gaussian elimination. The default values for pivot processing are used for IPARM. Input matrix $A$ is stored in profile-in skyline storage mode. Output matrix $A$ is in $LDL^\top$ factored form with $D^{-1}$ on the diagonal, and is stored in diagonal-out skyline storage mode. It is the same as output matrix $A$ in Example 1.

### Call Statement and Input:

```
N A NA IDIAG IPARM RPARM AUX AUX BX LDBX MBX
9, A, 33, IDIAG, IPARM, RPARM, AUX, 39, BX, 12, 3
A = (1.0, 1.0, 2.0, 1.0, 2.0, 3.0, 3.0, 1.0, 2.0, 3.0, 4.0, 1.0,
      2.0, 3.0, 4.0, 1.0, 2.0, 3.0, 3.0, 4.0, 5.0, 1.0, 2.0, 3.0,
      1.0, 2.0, 3.0, 4.0, 5.0, 3.0, 7.0, 1.0, 2.0, 3.0, 4.0)
IDIAG = (1, 3, 6, 10, 14, 19, 22, 29, 33, 34)
IPARM = (1, 10, 0, 1, 0, ..., ..., ..., ..., 0, ..., ...
         0, ..., ..., ..., ..., ..., ..., ..., 0, ..., ...)
RPARM = (not relevant)
```

![](img/5b0f44f3be6048723819b26aed7f6f03_654_1.png)

### Output:

A = (same as output A in Example 1)
IDIAG = (same as input IDIAG in Example 1)
IPARM = (1, 10, 0, 1, 0, ..., ..., ..., 0, ..., ..., ..., 8,
         ..., ..., ..., 0, 0, 0, 0, 0, 9)
RPARM = ( ..., ..., ..., ..., ..., ..., 0, ...)
BX = (same as output BX in Example 1)

## Example 3

This example shows how to factor a 9 by 9 negative-definite symmetric sparse matrix $A$, solve the system $Ax = b$ with three right-hand sides, and compute the determinant of $A$. It uses Gaussian elimination. (Default values for pivot processing are not used for IPARM because $A$ is negative-definite.) Input matrix $A$, shown here, is stored in diagonal-out skyline storage mode. Matrix $A$ is:

![](img/5b0f44f3be6048723819b26aed7f6f03_654_2.png)

![](img/5b0f44f3be6048723819b26aed7f6f03_655_0.png)

Output matrix A, shown here, is in LDL^{T} factored form with D^{-1} on the diagonal, and is stored in diagonal-out skyline storage mode. Matrix A is:

![](img/5b0f44f3be6048723819b26aed7f6f03_655_1.png)

### Call Statement and Input:

```
N  A  NA IDIAG  IPARM  RPARM AUX  NAUX  BX  LDBX MBX
CALL DSKFS(9, A, 33, IDIAG, IPARM, RPARM, AUX, 39, BX, 12, 3)
A        = (-1.0, -2.0, -1.0, -3.0, -2.0, -1.0, -4.0, -3.0, -2.0,
            -1.0, -4.0, -3.0, -2.0, -1.0, -5.0, -4.0, -3.0, -2.0,
            -1.0, -3.0, -2.0, -1.0, -7.0, -3.0, -5.0, -4.0, -3.0,
            -2.0, -1.0, -4.0, -3.0, -2.0, -1.0)
IDIAG    = (1, 2, 4, 7, 11, 15, 20, 23, 30, 34)
IPARM    = (1, 10, 0, 0, 0, ·, ·, ·, ·, 1, 0, -1, -1, -1, -1, ·,
            ·, ·, ·, ·, ·, ·, ·, ·, ·, ·, ·, ·, ·, ·, ·, ·)
RPARM    = ( ·, ·, ·, ·, ·, ·, ·, ·, ·, ·, ·, 10^{-15}, ·, ·, ·,
            ·, ·, ·, ·, ·, ·, ·, ·, ·, ·, ·, ·, ·, · )
BX       =(same as input BX in Example 1)
```

### Output:

```
A        = (-1.0, -1.0, 1.0, -1.0, 1.0, 1.0, -1.0, 1.0,
            1.0, 1.0,
            -1.0, 1.0, 1.0, 1.0, -1.0, 1.0, 1.0, 1.0, -1.0, 1.0,
            1.0, -1.0, 1.0, 1.0, 1.0, 1.0, 1.0, -1.0, 1.0, 1.0,
            1.0)
IDIAG    =(same as input)
IPARM    = (1, 10, 0, 0, 0, ·, ·, ·, ·, 1, 0, -1, -1, -1, 1, 8,
            ·, ·, ·, ·, ·, ·, 9, 0, 0, 0, 0)
RPARM    = ( ·, ·, ·, ·, ·, ·, ·, ·, ·, ·, 10^{-15}, ·, ·, ·,
            ·, ·, ·, ·, ·, 7.0, -1.0, 0.0, ·, ·, ·, ·, ·, · )
BX       = [+1.00 -2.00 -3.00
            +1.00 -2.00 -3.00
            +1.00 -2.00 -3.00
            -1.00 -2.00 -3.00
            -1.00 -2.00 -3.00
            -1.00 -2.00 -3.00
            -1.00 -2.00 -3.00
            -1.00 -2.00 -3.00]
```

## Example 4

This example shows how to factor the first six rows and columns, referred to as matrix $A'$, of the 9 by 9 symmetric sparse matrix $A$ from Example 1 and compute the determinant of $A'$. It uses Gaussian elimination. Input matrix $A'$, shown here, is stored in diagonal-out skyline storage mode. Input matrix $A'$ is:

$$
\begin{bmatrix}
1.0 & 1.0 & 1.0 & 1.0 & 0.0 & 0.0 \\
1.0 & 2.0 & 2.0 & 2.0 & 1.0 & 1.0 \\
1.0 & 2.0 & 3.0 & 3.0 & 2.0 & 2.0 \\
1.0 & 2.0 & 3.0 & 4.0 & 3.0 & 3.0 \\
0.0 & 1.0 & 2.0 & 3.0 & 4.0 & 4.0 \\
0.0 & 1.0 & 2.0 & 3.0 & 4.0 & 5.0
\end{bmatrix}
$$

Output matrix $A'$, shown here, is in $L D L^{T}$ factored form with $D^{-1}$ on the diagonal, and is stored in diagonal-out skyline storage mode. Output matrix $A'$ is:

$$
\begin{bmatrix}
1.0 & 1.0 & 1.0 & 1.0 & 0.0 & 0.0 \\
1.0 & 1.0 & 1.0 & 1.0 & 1.0 & 1.0 \\
1.0 & 1.0 & 1.0 & 1.0 & 1.0 & 1.0 \\
1.0 & 1.0 & 1.0 & 1.0 & 1.0 & 1.0 \\
0.0 & 1.0 & 1.0 & 1.0 & 1.0 & 1.0 \\
0.0 & 1.0 & 1.0 & 1.0 & 1.0 & 1.0
\end{bmatrix}
$$

### Call Statement and Input:

```
N   A   NA  IDIAG  IPARM  RPARM  AUX  NAUX  BX   LDBX   MBX
 |   |   |     |      |      |    |     |    |     |
CALL DSKFS ( 6 , A , 33 , IDIAG , IPARM , RPARM , AUX , 27 , BX , LDBX , MBX )
```

```
A     =(same as input A in Example 1)
IDIAG = ( 1, 2, 4, 7, 11, 15, 20 )
IPARM = ( 1, 11, 0, 0, 0, , , , , , 0, , , , , , , , , , ,
        , , , , , , , , , , , , , . )
RPARM =(not relevant)
BX    =(not relevant)
LDBX  =(not relevant)
MBX   =(not relevant)
```

### Output:

```
A     = ( 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0,
          1.0, 1.0,
          1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 3.0, 2.0, 1.0,
          7.0, 3.0, 5.0, 4.0, 3.0, 2.0, 1.0, 4.0, 3.0, 2.0, 1.0 )
IDIAG =(same as input)
IPARM = ( 1, 11, 0, 0, 0, , , , , , 0, , , , , , , , , , 6,
          , , , , , , 0, 0, 0, 0, 6 )
RPARM = ( , , , , , , , , , , , , , , , , , , , , , , , , , ,
          , , 5.0, 1.0, 0.0, , , , , , , , , , . )
BX    =(same as input)
LDBX  =(same as input)
MBX   =(same as input)
```
