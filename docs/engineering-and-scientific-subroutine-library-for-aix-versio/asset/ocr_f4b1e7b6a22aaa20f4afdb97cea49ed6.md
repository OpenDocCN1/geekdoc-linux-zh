# SSPMV DSPMV CHPMV ZHPMV SSYMV DSYMV CHEMV ZHEMV SSLMX DSLMX

```
Y = (36.0, 54.0, 36.0)
```

# Example 3

This example shows vector $\mathbf{x}$ and $\mathbf{y}$ with positive stride and a complex Hermitian matrix $A$ of order 3, stored in lower-packed storage mode. Matrix $A$ is:

![](bbox=[0.3, 0.17, 0.7, 0.24])

Note: On input, the imaginary parts of the diagonal elements of the complex Hermitian matrix $A$ are assumed to be zero, so you do not have to set these values.

# Call Statement and Input:

```
UPLO N ALPHA AP X INCX BETA Y INCY
   | | | | | | |
CALL CHPMV( 'L' , 3 , ALPHA , AP , X , 1 , BETA , Y , 2 )
ALPHA = (1.0, 0.0)
AP = ((1.0, . ) , (3.0, -5.0), (2.0, 3.0), (7.0, . ),
     (4.0, 8.0), (6.0, . ) )
X = ((1.0, 2.0), (4.0, 2.0), (3.0, 4.0))
BETA = (1.0, 0.0)
Y = ((1.0, 0.0), . , (2.0, -1.0), . , (2.0, 1.0))
```

# Output:

```
Y = ((32.0, 21.0), . , (87.0, -8.0), . , (32.0, 64.0))
```

# Example 4

This example shows vector $\mathbf{x}$ and $\mathbf{y}$ having strides of opposite signs. For $\mathbf{x}$, which has negative stride , processing begins at element $\mathbf{x}(5)$, which is (1.0, 2.0). The complex Hermitian matrix $A$ of order 3 is stored in upper-packed storage mode. It uses the same input matrix $A$ as in Example 3.

Note: On input, the imaginary parts of the diagonal elements of the complex Hermitian matrix $A$ are assumed to be zero, so you do not have to set these values.

# Call Statement and Input:

```
UPLO N ALPHA AP X INCX BETA Y INCY
   | | | | | | |
CALL CHPMV( 'U' , 3 , ALPHA , AP , X , -2 , BETA , Y , 2 )
ALPHA = (1.0, 0.0)
AP = ((1.0, . ), (3.0, 5.0), (7.0, . ), (2.0, -3.0),
     (4.0, -8.0), (6.0, . ) )
X = ((3.0, 4.0), . , (4.0, 0.0), . , (1.0, 2.0))
BETA = (0.0, 0.0)
Y = (not relevant)
```

# Output:

```
Y = ((31.0, 21.0), . , (85.0, -7.0), . , (30.0, 63.0))
```

# Example 5

This example shows vectors $\mathbf{x}$ and $\mathbf{y}$ with positive strides and a real symmetric matrix $A$ of order 3, stored in lower storage mode. It uses the same input matrix $A$ as in Example 1.