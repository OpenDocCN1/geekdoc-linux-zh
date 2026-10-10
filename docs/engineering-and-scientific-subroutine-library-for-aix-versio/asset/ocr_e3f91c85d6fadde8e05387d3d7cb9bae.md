# SZAXPY, DZAXPY, CZAXPY, and ZZAXPY

**Call Statement and Input:**

```
```
N ALPHA X INCX Y INCY Z INCZ
| | | | | | | |
CALL SZAXPY( 5 , 2.0 , X , 0 , Y , 1 , Z , -1 )
X = (1.0)
Y = (5.0, 4.0, 3.0, 2.0, 1.0)
```
```

**Output:**

```
```
Z = (3.0, 4.0, 5.0, 6.0, 7.0)
```
```

# Example 4

This example shows a vector, *y*, with 0 stride. *y* is treated like a vector of length *n*, all of whose elements are the same as the single element in *y*.

**Call Statement and Input:**

```
```
N ALPHA X INCX Y INCY Z INCZ
| | | | | | | |
CALL SZAXPY( 5 , 2.0 , X , 1 , Y , 0 , Z , 1 )
X = (1.0, 2.0, 3.0, 4.0, 5.0)
Y = (5.0)
```
```

**Output:**

```
```
Z = (7.0, 9.0, 11.0, 13.0, 15.0)
```
```

# Example 5

This example shows how SZAXPY can be used to compute a scalar value. In this case, vectors *x* and *y* contain scalar values. The strides of all vectors, *x*, *y*, and *z*, are 0. The number of elements to be processed, *n*, is 1.

**Call Statement and Input:**

```
```
N ALPHA X INCX Y INCY Z INCZ
| | | | | | | |
CALL SZAXPY( 1 , 2.0 , X , 0 , Y , 0 , Z , 0 )
X = (1.0)
Y = (5.0)
```
```

**Output:**

```
```
Z = (7.0)
```
```

# Example 6

This example shows vectors *x* and *y*, containing complex numbers and having positive strides.

**Call Statement and Input:**

```
```
N ALPHA X INCX Y INCY Z INCZ
| | | | | | | |
CALL CZAXPY( 3 ,ALPHA, X , 1 , Y , 2 , Z , 1 )
ALPHA = (2.0, 3.0)
X = ((1.0, 2.0), (2.0, 0.0), (3.0, 5.0))
Y = ((1.0, 1.0), . , (0.0, 2.0), . , (5.0, 4.0))
```
```

**Output:**

```
```
Z = ((-3.0, 8.0), (4.0, 8.0), (-4.0, 23.0))
```
```