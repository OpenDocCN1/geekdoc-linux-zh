# SCOND and SCORD

# Example 4

This example shows how the output from Example 1 differs when a negative stride is specified for the sequence in H. By reversing the H sequence, the correlation is computed.

Call Statement and Input:

```
H   INCH  X   INCX  Y   INCY  NH   NX  IYO   NY
|     |     |      |     |      |      |      |
CALL SCOND( H , -1 , X , 1 , Y , 1 , 4 , 8 , 0 , 11 )
H      = (1.0, 2.0, 3.0, 4.0)
X      = (11.0, 12.0, 13.0, 14.0, 15.0, 16.0, 17.0, 18.0)
```

Output:

```
Y      = (44.0, 81.0, 110.0, 130.0, 140.0, 150.0, 160.0, 170.0,
         104.0, 53.0, 18.0)
```

# Example 5

This example shows how to compute the autoconvolution of a sequence by letting the two input sequences for H and X be the same. (X is specified for both arguments in the calling sequence.)

Call Statement and Input:

```
H   INCH  X   INCX  Y   INCY  NH   NX  IYO   NY
|     |     |      |     |      |      |      |
CALL SCOND( X , 1 , X , 1 , Y , 1 , 4 , 4 , 0 , 7 )
X      = (11.0, 12.0, 13.0, 14.0)
```

Output:

```
Y      = (121.0, 264.0, 430.0, 620.0, 505.0, 364.0, 196.0)
```

# Example 6

This example shows how to compute a correlation of a sequence in H with a sequence in X, where both sequences are ramp functions.

Call Statement and Input:

```
H   INCH  X   INCX  Y   INCY  NH   NX   IYO   NY
|     |     |      |     |      |      |       |
CALL SCORD( H , 1 , X , 1 , Y , 1 , 4 , 8 , -3 , 11 )
H      = (1.0, 2.0, 3.0, 4.0)
X      = (11.0, 12.0, 13.0, 14.0, 15.0, 16.0, 17.0, 18.0)
```

Output:

```
Y      = (44.0, 81.0, 110.0, 130.0, 140.0, 150.0, 160.0, 170.0,
         104.0, 53.0, 18.0)
```

# Example 7

This example shows how the output from Example 6 differs when the value for IYO is -5 rather than -3 and NY is 15 rather than 11. The output has two zeros at the beginning and end of the sequence, for points outside the range of nonzero output.

Call Statement and Input:

```
H   INCH  X   INCX  Y   INCY  NH   NX   IYO   NY
|     |     |      |     |      |      |       |
CALL SCORD( H , 1 , X , 1 , Y , 1 , 4 , 8 , -5 , 15 )
```