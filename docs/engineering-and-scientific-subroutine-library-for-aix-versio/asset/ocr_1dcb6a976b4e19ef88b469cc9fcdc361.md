# SSPMV DSMPV CHPMV ZHPMV SSYMV DSYMV CHEMV ZHEMV SSLMX DSLMX

# Call Statement and Input:

```
```
        UPLO   N    ALPHA   A     LDA  X    INCX BETA Y INCY
         |      |     |       |     |     |      |     |   |
   CALL SSYMV( 'L' , 3 , 1.0 , A , 3 , X , 1 , 1.0 , Y , 2 )
```
```

$A = \begin{bmatrix} 8.0 & . & . \\ 4.0 & 6.0 & . \\ 2.0 & 7.0 & 3.0 \end{bmatrix}$

$X = (3.0,\ 2.0,\ 1.0)$
$Y = (5.0,\ .,\ 3.0.,\ .,\ 2.0)$

# Output:

$Y = (39.0,\ .,\ 34.0.,\ .,\ 25.0)$

# Example 6

This example shows vector x and y having strides of opposite signs. For x, which has negative stride, processing begins at element X(5), which is 1.0. The real symmetric matrix A of order 3 is stored in upper storage mode. It uses the same input matrix A as in Example 1.

# Call Statement and Input:

```
```
        UPLO   N    ALPHA   A     LDA  X    INCX BETA Y INCY
         |      |     |       |     |     |      |     |   |
   CALL SSYMV( 'U' , 3 , 1.0 , A , 4 , X , -2 , 2.0 , Y , 1 )
```
```

$A = \begin{bmatrix} 8.0 & 4.0 & 2.0 \\ . & 6.0 & 7.0 \\ . & . & 3.0 \\ . & . & . \end{bmatrix}$

$X = (4.0,\ .,\ 2.0.,\ .,\ 1.0)$
$Y = (6.0,\ 5.0,\ 4.0)$

# Output:

$A = (36.0,\ 54.0,\ 36.0)$

# Example 7

This example shows vector x and y with positive stride and a complex Hermitian matrix A of order 3, stored in lower storage mode. It uses the same input matrix A as in Example 3.

**Note:** On input, the imaginary parts of the diagonal elements of the complex Hermitian matrix A are assumed to be zero, so you do not have to set these values.

# Call Statement and Input:

```
```
        UPLO   N    ALPHA   A     LDA  X    INCX BETA Y INCY
         |      |     |       |     |     |      |     |   |
   CALL CHEMV( 'L' , 3 , ALPHA , A , 3 , X , 1 , BETA , Y , 2 )
```
```

$ALPHA = (1.0,\ 0.0)$