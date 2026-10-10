# SCRFT2 and DCRT2

Two invocations of this subroutine are necessary:

+   1.  With $init \neq 0$, the subroutine tests and initializes arguments of the program,  
+           setting up the *aux1* working storage.
+   2.  With $init = 0$, the subroutine checks that the initialization arguments in the
+           *aux1* working storage correspond to the present arguments, and if so, performs
+           the calculation of the Fourier transform.

# ## Error Conditions

**Resource Errors:** Error 2015 is unrecoverable, *nau x2* = 0, and unable to allocate work area.

**Computational Errors:** None

+   **Input-Argument Errors:**
+   1.  *n1* > 37748736
+   2.  *n2* > 37748736
+   3.  *inc2x* < (*n1*)/2+1
+   4.  *inc2y* < *n1*+2
+   5.  *scale* = 0.0
+   6.  *isign* = 0
+   7.  The subroutine has not been initialized with the present arguments.
+   8.  The length of one of the transforms in *n1* or *n2* is not an allowable value.
+           Return code 1 is returned if error 2030 is recoverable.
+   9.  *naux1* is too small—that is, less than the minimum required value. Return
+           code 1 is returned if error 2015 is recoverable.
+   10. Error 2015 is recoverable or *naux2*<0, and *naux2* is too small—that is, less than
+           the minimum required value. Return code 1 is returned if error 2015 is
+           recoverable.

# ### Example 1

This example shows how to compute a two-dimensional transform. The arrays are declared as follows:

```
```
REAL*4      Y(0:13, 0:7)
COMPLEX*8   X(0:6, 0:7)
REAL*8      AUX1(1000), AUX2(1000), AUX3(1)
```
```

First, initialize AUX1 using the calling sequence shown below with INIT $\neq$ 0. Then use the same calling sequence with INIT = 0 to do the calculation.

# Call Statement and Input:

```
```
INIT      X INC2X  Y  INC2Y  N1  N2  ISIGN SCALE   AUX1  NAUX1  AUX2  NAUX2  AUX3   NAUX3
CALL SCRFT2(INIT, X ,  7  ,  Y , 14  , 12  , 8  , -1, SCALE , AUX1 , 1000 , AUX2 , 1000 , AUX3 ,   0 )
```
```

```
```
INIT      = 1 (for initialization)
INIT      = 0 (for computation)
SCALE     = 1./96.0
X is an array with 7 rows and 8 columns with (1.0, 0.0) in all locations.
```
```

**Output:**

```
```
1.0 0.0 0.0 0.0 0.0 0.0 0.0 0.0
0.0 0.0 0.0 0.0 0.0 0.0 0.0 0.0
0.0 0.0 0.0 0.0 0.0 0.0 0.0 0.0
0.0 0.0 0.0 0.0 0.0 0.0 0.0 0.0
0.0 0.0 0.0 0.0 0.0 0.0 0.0 0.0
0.0 0.0 0.0 0.0 0.0 0.0 0.0 0.0
```
```