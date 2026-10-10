# **Example 6**

This example shows vector *x* and *y* having strides of opposite signs. For *x*, which has negative stride, processing begins at element *X*(*5*), which is 3.0. The real symmetric matrix *A* of order 3 is stored in upper storage mode. It uses the same input matrix *A* as in Example 1.

# **Call Statement and Input:**

```
```
UPLO N ALPHA X INCX Y INCY A LDA
I I I I I I I I
CALL SSPR2 ( 'U' , 3 , 1.0 , X , -2 , Y , 2 , A , 4 )
```

X = ( 1.0 , . , 2.0 , . , 3.0 )

Y = ( 5.0 , . , 3.0 , . , 2.0 )
```

A = 

$$
\left[\begin{array}{ccc} 8.0 & 4.0 & 2.0 \\ . & 6.0 & 7.0 \\ . & . & 3.0 \\ . & . & . \end{array}\right]
$$

**Output:**

```
A = 

$$
\left[\begin{array}{ccc} 38.0 & 23.0 & 13.0 \\ . & 18.0 & 14.0 \\ . & . & 7.0 \\ . & . & . \end{array}\right]
$$
```

# **Example 7**

This example shows vector *x* and *y* with positive stride, and a complex Hermitian matrix *A* of order 3, stored in lower storage mode. It uses the same input matrix *A* as in Example 3.

**Note:** On input, the imaginary parts of the diagonal elements of the complex Hermitian matrix *A* are assumed to be zero, so you do not have to set these values. On output, if $\alpha \neq$ zero, the imaginary parts of the diagonal elements are set to zero.

# **Call Statement and Input:**

```
```
UPLO N ALPHA X INCX Y INCY A LDA
I I I I I I I I
CALL CHER2 ( 'L' , 3 , ALPHA , X , 1 , Y , 2 , A , 3 )
```

ALPHA = (1.0, 0.0)

X = ((1.0, 2.0), (4.0, 0.0), (3.0, 4.0))

Y = ((1.0, 0.0), . , (2.0, -1.0), . , (2.0, 1.0))
```

A = 

$$
\left[\begin{array}{ccc} (1.0 , .) & . & . \\ (3.0 , -5.0) & (7.0 , .) & . \\ (2.0 , 3.0) & (4.0 , 8.0) & (6.0 , .) \end{array}\right]
$$

**Output:**

```
A = 

$$
\left[\begin{array}{ccc} (3.0 , 0.0) & (23.0 , 0.0) & . \\ (7.0 , -10.0) & (14.0 , 23.0) & (26.0 , 0.0) \\ (9.0 , 4.0) & . & . \end{array}\right]
$$
```