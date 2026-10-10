
## SSCAL, DSCAL, CSCAL, ZSCAL, CSSCAL, and ZDSCAL—Multiply a Vector X by a Scalar and Store in the Vector X

These subprograms perform the following computation, using the scalar $\alpha$ and the vector $x$:
$x \leftarrow \alpha x$

### Table 54. Data Types

| $\alpha$ | $x$ | Subprogram |
|:---:|:---:|:---:|
| Short-precision real | Short-precision real | SSCAL |
| Long-precision real | Long-precision real | DSCAL |
| Short-precision complex | Short-precision complex | CSCAL |
| Long-precision complex | Long-precision complex | ZSCAL |
| Short-precision real | Short-precision complex | CSSCAL |
| Long-precision real | Long-precision complex | ZDSCAL |

### Syntax

| Fortran | `CALL SSCAL \| DSCAL \| CSCAL \| ZSCAL \| CSSCAL \| ZDSCAL (n, alpha, x, incx)` |
|:---|:---|
| C and C++ | `sscal \| dscal \| cscal \| zscal \| cscal \| zdscl (n, alpha, x, incx);` |

- **On Entry:**
    - $n$ is the number of elements in vector $x$. Specified as: a fullword integer; $n \geq 0$.
    - $\alpha$ is the scalar $\alpha$. Specified as: a number of the data type indicated in Table 54.
    - $x$ is the vector $x$ of length $n$. Specified as: a one-dimensional array of (at least) length $1+ (n-1) |incx|$, containing numbers of the data type indicated in Table 54.
    - $incx$ is the stride for vector $x$. Specified as: a fullword integer. It can have any value.

- **On Return:**
    - $x$ is the vector $x$ of length $n$, containing the result of the computation $\alpha x$. Returned as: a one-dimensional array, containing numbers of the data type indicated in Table 54.

> **Note**: The fastest way in ESSL to zero out contiguous (stride 1) arrays is to call CSSCAL or DSCAL, specifying $incx = 1$ and $\alpha = 0$.

### Function

The computation is expressed as follows:

![](img/5b0f44f3be6048723819b26aed7f6f03_270_0.png)

See reference [81]. If $n$ is 0, no computation is performed. For CSCAL, intermediate results are accumulated in long precision.

### Error Conditions

- Computational Errors: None
- Input-Argument Errors: $n < 0$

### Example 1

This example shows a vector, $x$, with a stride of 1.

**Call Statement and Input:**

```text
N ALPHA X INCX
CALL SSCAL( 5 , 2.0 , X , 1 )
X = (1.0, 2.0, 3.0, 4.0, 5.0)
```

**Output:**

```text
X = (2.0, 4.0, 6.0, 8.0, 10.0)
```

### Example 2

This example shows vector, $x$, with a stride greater than 1.

**Call Statement and Input:**

```text
N ALPHA X INCX
CALL SSCAL( 5 , 2.0 , X , 2 )
X = (1.0, ., 2.0, ., 3.0, ., 4.0, ., 5.0)
```

**Output:**

```text
X = (2.0, ., 4.0, ., 6.0, ., 8.0, ., 10.0)
```

### Example 3

This example illustrates that when the strides for two similar computations (Example 1 and Example 3) have the same absolute value but have opposite signs, the output is the same. This example is the same as Example 1, except the stride for $x$ is negative (−1). For performance reasons, it is better to specify the positive stride. For $x$, processing begins at element $X(5)$, which is $5.0$, and results are stored beginning at the same element.

**Call Statement and Input:**

```text
N ALPHA X INCX
CALL SSCAL( 5 , 2.0 , X , -1 )
X = (1.0, 2.0, 3.0, 4.0, 5.0)
```

**Output:**

```text
X = {2.0, 4.0, 6.0, 8.0, 10.0}
```

### Example 4

This example shows how SSCAL can be used to compute a scalar value. In this case, input vector *x* contains a scalar value, and the stride is 0. The number of elements to be processed, *n*, is 1.

**Call Statement and Input:**

```text
N  ALPHA  X  INCX
 |   |      |   |
CALL SSCAL( 1, 2.0, X, 0 )
X = {1.0}
```

**Output:**

```text
X = {2.0}
```

### Example 5

This example shows a scalar, *α*, and a vector, *x*, containing complex numbers, where vector *x* has a stride of 1.

**Call Statement and Input:**

```text
N  ALPHA  X  INCX
 |    |     |   |
CALL CSCAL( 3, ALPHA, X, 1 )
ALPHA = {2.0, 3.0}
X = {{1.0, 2.0}, {2.0, 0.0}, {3.0, 5.0}}
```

**Output:**

```text
X = {{-4.0, 7.0}, {4.0, 6.0}, {-9.0, 19.0}}
```

### Example 6

This example shows a scalar, *α*, containing a real number, and a vector, *x*, containing complex numbers, where vector *x* has a stride of 1.

**Call Statement and Input:**

```text
N  ALPHA  X  INCX
 |   |      |   |
CALL CSSCAL( 3, 2.0, X, 1 )
X = {{1.0, 2.0}, {2.0, 0.0}, {3.0, 5.0}}
```

**Output:**

```text
X = {{2.0, 4.0}, {4.0, 0.0}, {6.0, 10.0}}
```

## SSWAP, DSWAP, CSWAP, and ZSWAP—Interchange the Elements of Two Vectors

These subprograms interchange the elements of vectors $x$ and $y$.

$y \leftrightarrow x$

### Table 55. Data Types

| x, y | Subprogram |
| :--- | :--- |
| Short-precision real | SSWAP |
| Long-precision real | DSWAP |
| Short-precision complex | CSWAP |
| Long-precision complex | ZSWAP |

### Syntax

| Fortran | `CALL SSWAP \| DSWAP \| CSWAP \| ZSWAP (n, x, incx, y, incy)` |
|:---|:---|
| C and C++ | `sswap \| dswap \| cswap \| zswap (n, x, incx, y, incy);` |

- **On Entry:**
    - $n$ is the number of elements in vectors $x$ and $y$. Specified as: a fullword integer; $n \geq 0$.
    - $x$ is the vector $x$ of length $n$. Specified as: a one-dimensional array of (at least) length $1+(n-1) |incx|$, containing numbers of the data type indicated in Table 55.
    - $incx$ is the stride for vector $x$. Specified as: a fullword integer. It can have any value.
    - $y$ is the vector $y$ of length $n$. Specified as: a one-dimensional array of (at least) length $1+(n-1) |incy|$, containing numbers of the data type indicated in Table 55.
    - $incy$ is the stride for vector $y$. Specified as: a fullword integer. It can have any value.

- **On Return:**
    - $x$ is the vector $x$ of length $n$, containing the elements that were swapped from vector $y$. Returned as: a one-dimensional array, containing numbers of the data type indicated in Table 55.
    - $y$ is the vector $y$ of length $n$, containing the elements that were swapped from vector $x$. Returned as: a one-dimensional array, containing numbers of the data type indicated in Table 55.

- **Notes:**
    1. If you specify the same vector for $x$ and $y$, then $incx$ and $incy$ must be equal; otherwise, results are unpredictable.
    2. If you specify different vectors for $x$ and $y$, they must have no common elements; otherwise, results are unpredictable. See “Concepts” on page 55.

### Function

The elements of vectors **x** and **y** are interchanged as follows:

![](img/5b0f44f3be6048723819b26aed7f6f03_273_0.png)

See reference [81]. If *n* is 0, no elements are interchanged.

### Error Conditions

- Computational Errors: None
- Input-Argument Errors: *n* < 0

### Example 1

This example shows vectors **x** and **y** with positive strides.

**Call Statement and Input:**

```text
N ALPHA X INCX
CALL SSWAP( 5, X, 1, , Y, 2 )
X = (1.0, 2.0, 3.0, 4.0, 5.0)
Y = (-1.0, , -2.0, , -3.0, , -4.0, , -5.0)
```

**Output:**

```text
X = (-1.0, -2.0, -3.0, -4.0, -5.0)
Y = (1.0, , 2.0, , 3.0, , 4.0, , 5.0)
```

### Example 2

This example shows how to obtain output vectors **x** and **y** that are reverse copies of the input vectors **y** and **x**. You must specify strides with the same absolute value, but with opposite signs. For **y**, which has negative stride, processing begins at element Y(5), which is -5.0, and the results of the swap are stored beginning at the same element.

**Call Statement and Input:**

```text
N ALPHA X INCX
CALL SSWAP( 5, X, 1, , Y, -1 )
X = (1.0, 2.0, 3.0, 4.0, 5.0)
Y = (-1.0, -2.0, -3.0, -4.0, -5.0)
```

**Output:**

```text
X = (-5.0, -4.0, -3.0, -2.0, -1.0)
Y = (5.0, 4.0, 3.0, 2.0, 1.0)
```

### Example 3

This example shows how SSWAP can be used to interchange scalar values in vectors **x** and **y** by specifying 0 strides and the number of elements to be processed as 1.

**Call Statement and Input:**

```text
N      X      INCX      Y      INCY
         |        |           |        |
CALL SSWAP( 1 , X , 0 , Y , 0 )
X         =      (1.0)
Y         =      (-4.0)
```

**Output:**

```text
X         =      (-4.0)
Y         =      (1.0)
```

### Example 4

This example shows vectors $x$ and $y$, containing complex numbers and having positive strides.

**Call Statement and Input:**

```text
N      X      INCX      Y      INCY
         |        |           |        |
CALL CSWAP( 4 , X , 1 , Y , 2 )
X         =      ((1.0, 6.0), (2.0, 7.0), (3.0, 8.0), (4.0, 9.0))
Y         =      ((-1.0, -1.0), . , (-2.0, -2.0), . , (-3.0, -3.0), . ,
                   (-4.0, -4.0))
```

**Output:**

```text
X         =      ((-1.0, -1.0), (-2.0, -2.0), (-3.0, -3.0), (-4.0, -4.0))
Y         =      ((1.0, 6.0), . , (2.0, 7.0), . , (3.0, 8.0), . ,
                   (4.0, 9.0))
```
