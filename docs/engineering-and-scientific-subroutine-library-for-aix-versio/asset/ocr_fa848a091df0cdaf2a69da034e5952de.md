![](bbox=[0.278, 0.075, 0.655, 0.217])

# Example 2

This example shows another transform computation with different data using the same initialized array AUX1 in Example 1.

# Call Statement and Input:

```
INIT X INC2X Y INC2Y N1 N2 ISIGN SCALE AUX1 NAUX1 AUX2 NAUX2 AUX3 NAUX3
CALL SCRFT2( 0 , X , 7 , Y , 14 , 12 , 8 , -1 , SCALE , AUX1 , 1000 , AUX2 , 1000 , AUX3 , 0 )
```

SCALE = 1.0/96.0
X is an array with 7 rows and 8 columns having (96.0, 0.0) in location X(θ,θ) and (0.0, 0.0) in all others.

Output:

![](bbox=[0.277, 0.438, 0.654, 0.624])

# Example 3

This example shows the same array being used for input and output. The arrays are declared as follows:

```
REAL*8            Y(0:17,0:7)
COMPLEX*16        X(0:8,0:7)
REAL*8            AUX1(1000), AUX2(1000), AUX3(1)
```

Arrays X and Y are made equivalent by the following statement, making them occupy the same storage.

```
EQUIVALENCE (X,Y)
```

This requires $inc2y = 2(inc2x)$. First, initialize AUX1 using the calling sequence shown below with $INIT \neq 0$. Then use the same calling sequence with $INIT = 0$ to do the calculation.