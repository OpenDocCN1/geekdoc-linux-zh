```
AU = (2.0, 2.0, 4.0, 2.0, 4.0, 6.0, 2.0, 4.0, 6.0, 2.0, 4.0, 6.0, 4.0, 2.0, 4.0, 6.0, 2.0, 4.0, 4.0, 8.0, 8.0, 2.0, 4.0, 6.0, 8.0, 2.0, 4.0, 6.0, 4.0, 10.0, 8.0, 10.0, 16.0)
IDU = (1, 3, 6, 9, 13, 16, 21, 25, 33, 34)
AL = (0.0, 2.0, 0.0, 2.0, 4.0, 2.0, 4.0, 6.0, 0.0, 2.0, 0.0, 2.0, 4.0, 6.0, 8.0, 0.0, 2.0, 4.0, 6.0, 0.0, 2.0, 4.0, 6.0, 8.0, 0.0, 2.0, 4.0, 6.0, 8.0, 10.0, 8.0, 0.0)
IDL = (1, 3, 6, 10, 12, 17, 21, 26, 35, 36)
IPARM = (1, 110, 0, 1, 0, * * * * * * * * * * * * 0, * * * * * * * * * * * * 0, * * * * * * * * * * * *)
RPARM = (not relevant)
```

```
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

# Example 3

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