# SCRFT and DCRAFT

**Input-Argument Errors:**

+   1. *n* > 37748736
+   2. *m* ≤ 0
+   3. *inc2x* < *n*/2+1
+   4. *inc2y* < *n*
+   5. *scale* = 0.0
+   6. *isign* = 0
+   7. The subroutine has not been initialized with the present arguments.
+   8. The length of the transform in *n* is not an allowable value. Return code 1 is returned if error 2030 is recoverable.
+   9. *naux1* ≤ 13
+   10. *naux1* is too small—that is, less than the minimum required value. Return code 1 is returned if error 2015 is recoverable.
+   11. Error 2015 is recoverable or *naux2*≠0, and *naux2* is too small—that is, less than the minimum required value. Return code 1 is returned if error 2015 is recoverable.

# Example 1

This example uses the mixed-radix capability and shows how to compute a single transform. The arrays are declared as follows:

```
```
COMPLEX*8     X(0:6)
REAL*8       AUX1(50), AUX2(50), AUX3(1)
REAL*4       Y(0:11)
```
```

First, initialize `AUX1` using the calling sequence shown below with `INIT ≠ 0`. Then use the same calling sequence with `INIT = 0` to do the calculation.

> > **Note:** *X* shows the *n*/2+1 = 7 elements used in the computation.

# Call Statement and Input:

```
```
         INIT X INCX Y INCY N M ISIGN SCALE AUX1 NAUX1 AUX2 NAUX2 AUX3 NAUX3
         |	|	|	|	|	|	|	|	|	|	|	|	|	|	|	|	|	|
CALL SCRFT(INIT, X , Y , 0 , 0 , 12 , 1 , 1 , SCALE, AUX1 , 50 , AUX2 , 50 , AUX3 , 0 )

INIT     =  1 (for initialization)
INIT     =  0 (for computation)
SCALE    =  1.0
```
```

*X* contains the following sequence:

```
```
(1.0,  0.0)
(0.0,  0.0)
(0.0,  0.0)
(0.0,  0.0)
(0.0,  0.0)
(0.0,  0.0)
(0.0,  0.0)
```
```

**Output:**
Y = (1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0)

# Example 2

This example shows another transform computation with different data using the same initialized array `AUX1` as in Example 1.