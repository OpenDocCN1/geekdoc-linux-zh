# SRCFT2 and DRCFT2

# Example 2

This example shows another transform computation with different data using the same initialized array AUX1 in Example 1.

# Call Statement and Input:

INIT    X       INC2X   Y       INC2Y   N1      N2      ISIGN   SCALE   AUX1    NAUX1   AUX2    NAUX2   AUX3    NAUX3
CALL    SRCFT2(  0     , X   , 12  , Y   , 7   , 12  , 8  , 1   , SCALE, AUX1, 1000  , AUX2, 1000  , AUX3  , 0  )

SCALE       = 1.0
X is an array with 12 rows and 8 columns with 1.0 in all locations.

Output:  Y is an array with 7 rows and 8 columns having (96.0, 0.0) in location Y(0,0) and (0.0,0.0) in all others.

# Example 3

This example shows the same array being used for input and output, where $isign = -1$ and $scale = 1 / (\pi)(N2)$. The arrays are declared as follows:

```
COMPLEX*16    Y(0:8,0:7)
REAL*8       X(0:19,0:7)
REAL*8       AUX1(1000) , AUX2(1000) , AUX3(1)
```

Arrays X and Y are made equivalent by the following statement, making them occupy the same storage.

EQUIVALENCE  (X,Y)

This requires $inc2x \geq 2(inc2y)$. First, initialize AUX3 using the calling sequence shown below with INIT \neq 0. Then use the same calling sequence with INIT = 0 to do the calculation.

# Call Statement and Input:

INIT    X       INC2X   Y       INC2Y   N1      N2      ISIGN   SCALE   AUX1    NAUX1   AUX2    NAUX2   AUX3    NAUX3
CALL    DRCFT2( INIT, X   , 20  , Y   , 9   , 16  , 8  , -1  , SCALE, AUX1 , 1000  , AUX2, 1000  , AUX3  , 0  )

INIT      = 1 (for initialization)
INIT      = 0 (for computation)
SCALE     = 1.0/128.0

X   =   2.0  2.0 -2.0 -2.0  2.0  2.0 -2.0 -2.0
      2.0 -2.0 -2.0  2.0  2.0 +2.0 -2.0 -2.0
     -2.0  2.0  2.0 -2.0 -2.0 -2.0  2.0  2.0
     -2.0  2.0  2.0 -2.0 -2.0  2.0  2.0 -2.0
      2.0  2.0 -2.0 -2.0  2.0  2.0 +2.0 -2.0
      2.0 -2.0 -2.0  2.0  2.0 -2.0 -2.0  2.0
     -2.0  2.0  2.0 -2.0 -2.0  2.0  2.0 -2.0
      2.0  2.0 -2.0 -2.0  2.0  2.0 -2.0  2.0
     -2.0  2.0  2.0 -2.0 -2.0 -2.0  2.0  2.0
      2.0 -2.0 -2.0  2.0  2.0  2.0 +2.0 -2.0
     -2.0  2.0  2.0 -2.0 -2.0 -2.0  2.0  2.0
      2.0  2.0 -2.0 -2.0  2.0  2.0 -2.0  2.0
     -2.0 -2.0 -2.0  2.0  2.0 -2.0 -2.0  2.0
      .     .     .     .     .     .     .     .