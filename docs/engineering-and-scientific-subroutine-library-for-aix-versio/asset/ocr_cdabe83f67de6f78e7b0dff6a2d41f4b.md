# SCRFT and DCRAFT

```
0.0  -1.0
0.0  1.0
0.0  -1.0
0.0  1.0
0.0  -1.0
0.0  1.0
0.0  -1.0
```

# Example 4

This example shows the same array being used for input and output. The arrays are declared as follows:

```
COMPLEX*16  X(0:8,2)
REAL*8       AUX1(50), AUX2(16)
REAL*8       Y(0:17,2)
```

Arrays X and Y are made equivalent by the following statement, making them occupy the same storage:

```
EQUIVALENCE (X,Y)
```

This requires INCY2 = 2(INCX). First, initialize AUX1 using the calling sequence shown below with INIT = 0. Then use the same calling sequence with INIT = 0 to do the calculation.

# Call Statement and Input:

```
INIT  X INC2X Y  INC2Y  N   M ISIGN SCALE  AUX1  NAUX1 AUX2  NAUX2
  |     |    |     |    |     |    |      |       |      |      |
CALL DCRAFT(INIT, X , 9 , Y , 18 , 16 , 2 , -1 , SCALE, AUX1 , 50 , AUX2 , 16)
```

```
INIT     =  1 (for initialization)
INIT     =  0 (for computation)
SCALE    =  0.0625
```

X contains the following two sequences:

```
( 1.0,  0.0) ( 1.0,  0.0)
( 0.0,  1.0) ( 0.0, -1.0)
(-1.0,  0.0) (-1.0,  0.0)
( 0.0, -1.0) ( 0.0,  1.0)
( 1.0,  0.0) ( 1.0,  0.0)
( 0.0,  1.0) ( 0.0, -1.0)
(-1.0,  0.0) (-1.0,  0.0)
( 0.0, -1.0) ( 0.0,  1.0)
( 1.0,  0.0) ( 1.0,  0.0)
```

Output: Y contains the following two sequences:

```
0.0  0.0
0.0  0.0
0.0  0.0
0.0  0.0
0.0  1.0
0.0  0.0
0.0  0.0
0.0  0.0
0.0  0.0
0.0  0.0
0.0  0.0
0.0  0.0
0.0  0.0
0.0  0.0
0.0  0.0
1.0  0.0
0.0  0.0
0.0  0.0
0.0  0.0
```