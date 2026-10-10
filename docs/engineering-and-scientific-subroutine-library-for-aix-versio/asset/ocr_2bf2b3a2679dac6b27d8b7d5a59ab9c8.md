# SSPR, DSPR, CHPR, ZHPR, SSYR, DSYR, CHER, ZHER, SSLR1, and DSLR1

**Call Statement and Input:**

```
UPLO    N      ALPHA    X      INCX     AP
   |     |      |      |      |       |
CALL CHPR( 'L', 3, 1.0, X, 1, AP )
```

```
X      = ((1.0, 2.0), (4.0, 0.0), (3.0, 4.0))
AP     = ((1.0,  . ), (3.0, -5.0), (2.0, 3.0), (7.0,  . ),
         (4.0, 8.0), (6.0,  . ))
```

**Output:**

```
AP     = ((6.0, 0.0), (7.0, -13.0), (13.0, 1.0), (23.0, 0.0),
         (16.0, 24.0), (31.0, 0.0))
```

# Example 4

This example shows a vector *x* with a negative stride, and a complex Hermitian matrix *A* of order 3, stored in upper-packed storage mode. It uses the same input matrix *A* as in Example 3.

**Note:** On input, the imaginary parts of the diagonal elements of the complex Hermitian matrix *A* are assumed to be zero, so you do not have to set these values. On output, if *α* ≠ 0.0, they are set to zero.

**Call Statement and Input:**

```
UPLO    N      ALPHA    X      INCX     AP
   |     |      |      |      |       |
CALL CHPR( 'U', 3, 1.0, X, -2, AP )
```

```
X      = ((3.0, 4.0), . , (4.0, 0.0), . , (1.0, 2.0))
AP     = ((1.0,  . ), (3.0, 5.0), (7.0,  . ), (2.0, -3.0),
         (4.0, -8.0), (6.0,  . ))
```

**Output:**

```
AP     = ((6.0, 0.0), (7.0, 13.0), (23.0, 0.0), (13.0, -1.0),
         (16.0, -24.0), (31.0, 0.0))
```

# Example 5

This example shows a vector *x* with a positive stride, and a real symmetric matrix *A* of order 3, stored in lower storage mode. It uses the same input matrix *A* as in Example 1.

**Call Statement and Input:**

```
UPLO    N      ALPHA    X      INCX     A      LDA
   |     |      |      |      |       |      |
CALL SSYR( 'L', 3, 1.0, X, 1, A, 3 )
```

```
X      = (3.0, 2.0, 1.0)
```

```
A      = [ 8.0  .    .  ]
         [ 4.0  6.0  .  ]
         [ 2.0  7.0  3.0]
```

**Output:**

```
A      = [ 17.0  .    .   ]
         [ 10.0 10.0  .   ]
         [ 5.0  9.0  4.0 ]
```