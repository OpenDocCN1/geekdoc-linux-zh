
## Example 4

This example shows a vector, $y$, with 0 stride. $y$ is treated like a vector of length $n$, all of whose elements are the same as the single element in $y$.

Call Statement and Input:

```text
    N   X  INCX Y  INCY Z   INCZ
    |   |    |  |    |   |    |
CALL SVEM( 5 ,  X , 1  , Y , 0  ,  Z , 1  )

X       =  (1.0,  2.0,  3.0,  4.0,  5.0)
Y       =  (5.0)
```

Output:

```text
Z       =  (5.0,  10.0,  15.0,  20.0,  25.0)
```

## Example 5

This example shows the output vector, $z$, with 0 stride, where the vector $x$ has positive stride, and the vector $y$ has 0 stride. The number of elements to be processed, $n$, is greater than 1.

Call Statement and Input:

```text
    N   X  INCX Y  INCY Z   INCZ
    |   |    |  |    |   |    |
CALL SVEM( 5 ,  X , 1  , Y , 0  ,  Z , 0  )

X       =  (1.0,  2.0,  3.0,  4.0,  5.0)
Y       =  (5.0)
```

Output:

```text
Z       =  (25.0)
```

## Example 6

This example shows the output vector $z$, with 0 stride, where the vector $x$ has 0 stride, and the vector $y$ has negative stride. The number of elements to be processed, $n$, is greater than 1.

Call Statement and Input:

```text
    N   X  INCX Y  INCY Z   INCZ
    |   |    |  |    |   |    |
CALL SVEM( 5 ,  X , 0  , Y , -1 ,  Z , 0  )

X       =  (1.0)
Y       =  (5.0,  4.0,  3.0,  2.0,  1.0)
```

Output:

```text
Z       =  (5.0)
```

## Example 7

This example shows how SVEM can be used to compute a scalar value. In this case, vectors $x$ and $y$ contain scalar values. The strides of all vectors, $x$, $y$, and $z$, are 0. The number of elements to be processed, $n$, is 1.

Call Statement and Input:

```text
    N   X  INCX Y  INCY Z   INCZ
    |   |    |  |    |   |    |
CALL SVEM( 1 ,  X , 0  , Y , 0  ,  Z , 0  )

X       =  (1.0)
Y       =  (5.0)
```

Output:

```text
Z       =  (5.0)
```

## Example 8

This example shows vectors $\boldsymbol{x}$ and $\boldsymbol{y}$, containing complex numbers and having positive strides.

Call Statement and Input:

```text
N     X    INCX   Y     INCY   Z    INCZ
    |    |       |      |       |    |
CALL  CVEA( 3 ,  X ,  1  ,  Y ,  2  ,  Z ,  1  )
```

```text
X          =  ((1.0, 2.0), (3.0,  4.0), (5.0,  6.0))
Y          =  ((7.0, 8.0), . , (9.0, 10.0), . , (11.0, 12.0))
```

Output:

```text
Z = ((-9.0, 22.0), (-13.0,  66.0), (-17.0, 126.0))
```

# SYAX, DYAX, CYAX, ZYAX, CSYAX, and ZDYAX

## Multiply a Vector X by a Scalar and Store in a Vector Y

These subprograms perform the following computation, using the scalar $\alpha$ and vectors $\mathbf{x}$ and $\mathbf{y}$:

$y \leftarrow \alpha x$

### Table 59. Data Types

| $\alpha$ | x, y | Subprogram |
| :--- | :--- | :--- |
| Short-precision real | Short-precision real | SYAX |
| Long-precision real | Long-precision real | DYAX |
| Short-precision complex | Short-precision complex | CYAX |
| Long-precision complex | Long-precision complex | ZYAX |
| Short-precision real | Short-precision complex | CSYAX |
| Long-precision real | Long-precision complex | ZDYAX |

### Syntax

| Language | Statement |
| :--- | :--- |
| Fortran | `CALL SYAX \| DYAX \| CYAX \| ZYAX \| CSYAX \| ZDYAX (n, alpha, x, incx, y, incy)` |
| C and C++ | `syax \| dyax \| cyax \| zyx \| csyx \| zdyx (n, alpha, x, incx, y, incy);` |

### On Entry:

- $n$ is the number of elements in vector $x$ and $y$.
  - Specified as: a fullword integer; $n \geq 0$.
- $alpha$ is the scalar $\alpha$.
  - Specified as: a number of the data type indicated in Table 59.
- $x$ is the vector $x$ of length $n$.
  - Specified as: a one-dimensional array of (at least) length $1+(n-1)|incx|$, containing numbers of the data type indicated in Table 59.
- $incx$ is the stride for vector $x$.
  - Specified as: a fullword integer. It can have any value.
- $y$
  - See “On Return.”
- $incy$ is the stride for vector $y$.
  - Specified as: a fullword integer. It can have any value.

### On Return:

- $y$ is the vector $y$ of length $n$, containing the result of the computation $\alpha x$.
  - Returned as: a one-dimensional array of (at least) length $1+(n-1)|incy|$, containing numbers of the data type indicated in Table 59.

### Notes

1. If you specify the same vector for $x$ and $y$, then $incx$ and $incy$ must be equal; otherwise, results are unpredictable.
2. If you specify different vectors for $x$ and $y$, they must have no common elements; otherwise, results are unpredictable. See "Concepts" on page 55.

## Function

The computation is expressed as follows:

![](img/5b0f44f3be6048723819b26aed7f6f03_288_0.png)

See reference [81]. If $n$ is 0, no computation is performed. For CYAX, intermediate results are accumulated in long precision.

## Error Condition

**Computational Errors:** None

**Input-Argument Errors:** $n<0$

## Example 1

This example shows vectors $\mathbf{x}$ and $\mathbf{y}$ with positive strides.

Call Statement and Input:

```text
      N    ALPHA    X     INCX    Y    INCY
      |        |      |       |    |      |
CALL SYAX( 5 , 2.0 , X , 1 , Y , 2  )
X       =  (1.0, 2.0, 3.0, 4.0, 5.0)
```

Output:

```text
Y       =  (2.0, , 4.0, , 6.0, , 8.0, , 10.0)
```

## Example 2

This example shows vectors $\mathbf{x}$ and $\mathbf{y}$ that have strides of opposite signs. For $\mathbf{y}$, which has negative stride, results are stored beginning in element $Y(5)$.

Call Statement and Input:

```text
      N    ALPHA    X     INCX    Y    INCY
      |        |      |       |    |      |
CALL SYAX( 5 , 2.0 , X , 1 , Y , -1  )
X       =  (1.0, 2.0, 3.0, 4.0, 5.0)
```

Output:

```text
Y       =  (10.0, 8.0, 6.0, 4.0, 2.0)
```

## Example 3

This example shows a vector, $\mathbf{x}$, with 0 stride. $\mathbf{x}$ is treated like a vector of length $n$, all of whose elements are the same as the single element in $\mathbf{x}$.

Call Statement and Input:

```text
      N    ALPHA    X     INCX    Y    INCY
      |        |      |       |    |      |
CALL SYAX( 5 , 2.0 , X , 0 , Y , 1  )
X       =  (1.0)
```

Output:

```text
Y = {2.0, 2.0, 2.0, 2.0, 2.0}
```

## Example 4

This example shows how SYAX can be used to compute a scalar value. In this case both vectors x and y contain scalar values, and the strides for both vectors are 0. The number of elements to be processed, $n$, is 1.

Call Statement and Input:

```text
N   ALPHA X   INCX Y   INCY
1   |       |       |       |       |
CALL SYAX( 1, 2.0, X, 0, Y, 0 )
```

```text
X = {1.0}
```

Output:

```text
Y = {2.0}
```

## Example 5

This example shows a scalar, $\alpha$, and vectors x and y, containing complex numbers, where both vectors have a stride of 1.

Call Statement and Input:

```text
N   ALPHA X   INCX Y   INCY
3   |       |       |       |       |
CALL CYAX( 3, ALPHA, X, 1, Y, 1 )
```

```text
ALPHA = {2.0, 3.0}
X     = {{1.0, 2.0}, {2.0, 0.0}, {3.0, 5.0}}
```

Output:

```text
Y = {{-4.0, 7.0}, {4.0, 6.0}, {-9.0, 19.0}}
```

## Example 6

This example shows a scalar, $\alpha$, containing a real number, and vectors x and y, containing complex numbers, where both vectors have a stride of 1.

Call Statement and Input:

```text
N   ALPHA X   INCX Y   INCY
3   |       |       |       |       |
CALL CSYAX( 3, 2.0, X, 1, Y, 1 )
```

```text
X = {{1.0, 2.0}, {2.0, 0.0}, {3.0, 5.0}}
```

Output:

```text
Y = {{2.0, 4.0}, {4.0, 0.0}, {6.0, 10.0}}
```

# SZAXPY, DZAXPY, CZAXPY, and ZZAXPY

## Multiply a Vector X by a Scalar, Add to a Vector Y, and Store in a Vector Z

These subprograms perform the following computation, using the scalar $\alpha$ and vectors $x, y$, and $z$:

$z \leftarrow y + \alpha x$

### Table 60. Data Types

| $\alpha, x, y, z$ | Subprogram |
| :--- | :--- |
| Short-precision real | SZAXPY |
| Long-precision real | DZAXPY |
| Short-precision complex | CZAXPY |
| Long-precision complex | ZZAXPY |

### Syntax

| Language | Statement |
| :--- | :--- |
| Fortran | `CALL SZAXPY \| DZAXPY \| CZAXPY \| ZZAXPY (n, alpha, x, incx, y, incy, z, incz)` |
| C and C++ | `szaxpy \| dzaxpy \| czaxpy \| zzaxpy (n, alpha, x, incx, y, incy, z, incz);` |

### On Entry:

- $n$ is the number of elements in vectors $x, y$, and $z$.
  - Specified as: a fullword integer; $n \geq 0$.
- $alpha$ is the scalar $\alpha$.
  - Specified as: a number of the data type indicated in Table 60.
- $x$ is the vector $x$ of length $n$.
  - Specified as: a one-dimensional array of (at least) length $1 + (n - 1)|incx|$, containing numbers of the data type indicated in Table 60.
- $incx$ is the stride for vector $x$.
  - Specified as: a fullword integer. It can have any value.
- $y$ is the vector $y$ of length $n$.
  - Specified as: a one-dimensional array of (at least) length $1 + (n - 1)|incy|$, containing numbers of the data type indicated in Table 60.
- $incy$ is the stride for vector $y$.
  - Specified as: a fullword integer. It can have any value.
- $z$
  - See “On Return.”
- $incz$ is the stride for vector $z$.
  - Specified as: a fullword integer. It can have any value.

### On Return:

- $z$ is the vector $z$ of length $n$, containing the result of the computation $y + \alpha x$.
  - Returned as: a one-dimensional array of (at least) length $1 + (n - 1)|incz|$, containing numbers of the data type indicated in Table 60.

### Notes

1. If you specify the same vector for $x$ and $z$, then $incx$ and $incz$ must be equal; otherwise, results are unpredictable. The same is true for $y$ and $z$.
