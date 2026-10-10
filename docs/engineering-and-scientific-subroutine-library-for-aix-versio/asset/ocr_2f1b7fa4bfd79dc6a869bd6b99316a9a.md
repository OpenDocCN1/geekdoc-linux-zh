```
Y       =  (11.0, 70.0, 130.0, 150.0, 151.0, 72.0)
```

# **Example 2**

This example shows how to compute a correlation of a sequence in H with a sequence in X, where both sequences are ramp functions. It shows how a decimated output can be obtained, using the same input as "Example 6" on page 833 for SCORD and using a decimation interval ID = 2.

**Note:** For further examples of use, see the examples for SCORD on page 833. Because SCORD and SDCOR are functionally the same, their results are the same as long as the decimation interval ID = 1 for SDCOR.

# Call Statement and Input:

```
H INCH X INCX Y INCY NH NX IYO NY ID
|     |     |     |     |     |     |     |     |     |     |     |     |
CALL SDCOR( H, 1, X, 1, , Y, 1, , 4, 8, -3, 6, 2 )
H       =  (1.0, 2.0, 3.0, 4.0)
X       =  (11.0, 12.0, 13.0, 14.0, 15.0, 16.0, 17.0, 18.0)
```

# Output:

```
Y       =  (44.0, 110.0, 140.0, 160.0, 104.0, 18.0)
```

# **Example 3**

This example shows how to compute the same function as computed in *Example 1* on page 832 for SCOND. The input sequences and arguments are the same as that example, except a decimation interval ID = 1 is specified here for SDCON.

# Call Statement and Input:

```
H INCH X INCX Y INCY NH NX IYO NY ID
|     |     |     |     |     |     |     |     |     |     |     |     |
CALL SDCON( H, 1, X, 1, , Y, 1, , 4, 8, 0, 11, 1 )
H       =  (1.0, 2.0, 3.0, 4.0)
X       =  (11.0, 12.0, 13.0, 14.0, 15.0, 16.0, 17.0, 18.0)
```

# Output:

```
Y       =  (11.0, 34.0, 70.0, 120.0, 130.0, 140.0, 150.0, 160.0, 151.0, 122.0, 72.0)
```