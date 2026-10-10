
## SNAXPY and DNAXPY

`y` is a one- or two-dimensional array of (at least) length `(1+(n-1)(incyo))+(m-1)|incy|`, containing numbers of the data type indicated in Table 48 on page 220.

- *incyi* is the stride for *y* in the inner loop—that is, the stride identifying the elements in each vector *y*_i in *y*. Specified as: a fullword integer; *incyi* > 0 or *incyi* < 0.
- *incyo* is the stride for *y* in the outer loop—that is, the stride identifying each vector *y*_i in *y*. Specified as: a fullword integer; *incyo* ≥ 0.

### On Return

*y* is the vector (or matrix) *y*, containing the *y*_i vectors of length *m*, which contain the results of the *n* SAXPY or DAXPY computations, *y*_i + *α*_i *x*_i for *i* = 1, *n*. Returned as: a one- or two-dimensional array, containing numbers of the data type indicated in Table 48 on page 220.

### Note

Vector *y* must have no common elements with vector *a* or vector *x*; otherwise, results are unpredictable. See “Concepts” on page 55.

### Function

The SAXPY or DAXPY computations:

$$
y \leftarrow y + \alpha x
$$

are performed *n* times. This is expressed as follows:

$$
y_{i} \leftarrow y_{i} + \alpha_{i}x_{i} \quad \text{ for } i = 1, n
$$

where each *α*_i is a scalar value, contained in the vector *a*, and each *x*_i and *y*_i are vectors, contained in vectors (or matrices) *x* and *y*, respectively.

Each computation of SAXPY or DAXPY on page 210 uses the length of the *x*_i and *y*_i vectors, *n*_i, for its input argument, *n*. It also uses the strides for the inner loop, *incx*_i and *incy*_i, for its parameters *incx* and *incy*, respectively. See “Function” on page 211 for a description of how the computation is done.

The outer loop of the SNAXPY or DNAXPY computation uses the strides of *inca*, *incxo*, and *incyo* to locate the elements in *a* and vectors in *x* and *y* for each *i*-th computation. These are:

```
For i = 1, n:
a_{((i-1)inca+1)}  for inca ≥ 0
a_{((i-n)inca+1)}  for inca < 0
x_{((i-1)incx+1)}
y_{((i-1)incyo+1)}
```

If *m* or *n* is 0, no computation is performed.

### Error Conditions

**Computational Errors:** None

**Input-Argument Errors:**

1. *n* < 0
2. *m* < 0
3. *incxo* < 0
4. *incyi* = 0
5. *incyo* < 0

### Example 1

This example shows vectors, contained in matrices, with the stride of the inner loops *incx* and *incy* equal to 1.

**Call Statement and Input:**

```fortran
              N   M   A   INCA   X   INCXI  INCXO   Y   INCYI  INCYO
CALL  SNAXPY( 3 , 4 ,  A ,  1 ,  X ,  1 ,  10 ,  Y ,  1 ,   5  )
```

A = (3.0, 2.0, 4.0)

```
X = 1.0  4.0  3.0
     2.0  3.0  4.0
     3.0  2.0  2.0
     4.0  1.0  1.0
     .    .    .
     .    .    .
     .    .    .
     .    .    .
     .    .    .
```

```
Y = 4.0  1.0  3.0
     3.0  2.0  4.0
     2.0  3.0  2.0
     1.0  4.0  1.0
     .    .    .
```

**Output:**

```
Y = 7.0  9.0  15.0
     9.0  8.0  20.0
    11.0  7.0  10.0
    13.0  6.0   5.0
     .    .    .
```

### Example 2

This example shows vectors, contained in matrices, with a stride of the inner loop *incx* greater than 1.

**Call Statement and Input:**

```fortran
              N   M   A   INCA   X   INCXI  INCXO   Y   INCYI  INCYO
CALL  SNAXPY( 3 , 4 ,  A ,  1 ,  X ,  2 ,  10 ,  Y ,  1 ,   5  )
```

A = (3.0, 2.0, 4.0)

```
X = 1.0  4.0  3.0
     .    .    .
     2.0  3.0  4.0
     .    .    .
     3.0  2.0  2.0
     .    .    .
     4.0  1.0  1.0
     .    .    .
     .    .    .
```

```
Y = 4.0  1.0  3.0
     3.0  2.0  4.0
     2.0  3.0  2.0
     1.0  4.0  1.0
     .    .    .
```

**Output:**

Y = (same as output Y in Example 1)

### Example 3

This example shows vectors, contained in matrices, with a negative stride, *incy*, for the inner loop.

**Call Statement and Input:**

```fortran
              N   M   A   INCA   X   INCXI  INCXO   Y   INCYI  INCYO
CALL  SNAXPY( 3 , 4 ,  A ,  1 ,  X ,  1 ,  10 ,  Y , -1 ,  5  )
```

A = (3.0, 2.0, 4.0)

```
X = 1.0  4.0  3.0
     2.0  3.0  4.0
     3.0  2.0  2.0
     4.0  1.0  1.0
     .    .    .
     .    .    .
     .    .    .
     .    .    .
     .    .    .
     .    .    .
     .    .    .
     .    .    .
     .    .    .
```

```
Y = 1.0  4.0  1.0
     2.0  3.0  2.0
     3.0  2.0  4.0
     4.0  1.0  3.0
     .    .    .
```

**Output:**

```
Y = 13.0 6.0 5.0
     11.0 7.0 10.0
      9.0 8.0 20.0
      7.0 9.0 15.0
     .    .    .
```

### Example 4

This example shows vectors, contained in matrices, with a negative stride, *inca*, for vector *a*. For vector *a*, processing begins at element A(5), which is 3.0.

**Call Statement and Input:**

```fortran
              N   M   A   INCA   X   INCXI  INCXO   Y   INCYI  INCYO
CALL  SNAXPY( 3 , 4 ,  A , -2 , X ,  1 ,  10 ,  Y ,  1 ,  5  )
```

A = (4.0, . , 2.0, . , 3.0)

```
X = 1.0  4.0  3.0
     2.0  3.0  4.0
     3.0  2.0  2.0
     4.0  1.0  1.0
     .    .    .
     .    .    .
     .    .    .
     .    .    .
     .    .    .
```

```
Y = 4.0  1.0  3.0
     3.0  2.0  4.0
     2.0  3.0  2.0
     1.0  4.0  1.0
     .    .    .
```

**Output:**

Y = (same as output Y in Example 1)

## SNDOT and DNDOT—Compute Special Dot Products N Times

These subprograms compute one of the following special dot products *n* times:

- $s_i \leftarrow x_i^* \cdot y_i$  Store positive dot product
- $s_i \leftarrow -x_i^* \cdot y_i$  Store negative dot product
- $s_i \leftarrow s_i + x_i^* \cdot y_i$  Accumulate positive dot product
- $s_i \leftarrow s_i - x_i^* \cdot y_i$  Accumulate negative dot product
- for $i = 1, n$

where each $s_i$ is an element in vector $s$, and each $x_i$ and $y_i$ are vectors contained in vectors (or matrices) $x$ and $y$, respectively.

### Table 49. Data Types

| $s$, $x$, $y$ | Subprogram |
| :--- | :--- |
| Short-precision real | SNDOT |
| Long-precision real | DNDOT |

### Syntax

| Language | Syntax |
| :--- | :--- |
| Fortran | CALL SNDOT \| DNDOT (*n*, *m*, *s*, *isu*, *x*, *incx*, *y*, *incy*, *isu*) |
| C and C++ | sndot \| dndot (*n*, *m*, *s*, *isu*, *x*, *incx*, *y*, *incy*, *isu*); |

### On Entry

- *n* is the number of dot product computations to be performed and the number of elements in the vector *n*. Specified as: a fullword integer; *n* ≥ 0.
- *m* is the number of elements in vectors $x_i$ and $y_i$ for each dot product computation. Specified as: a fullword integer; *m* ≥ 0.
- *s* is the vector *s*, containing the *n* scalar values $s_i$, where:
  - If *isu* = 1 or 2, *s* is not used in the computation (no input value specified).
  - If *isu* = 3 or 4, $s_i$ is used in the computation (input value specified).
  - Specified as: a one-dimensional array of (at least) length $1+(n-1)\, \mathrm{incs}$, containing numbers of the data type indicated in Table 49.
- *incs* is the stride for vector *s*. Specified as: a fullword integer; *incs* > 0 or *incs* < 0.
- *isu* indicates the type of computation to perform, depending on the value specified:
  - If *isu* = 1, $s_i \leftarrow x_i^* \cdot y_i$
  - If *isu* = 2, $s_i \leftarrow -x_i^* \cdot y_i$
  - If *isu* = 3, $s_i \leftarrow s_i + x_i^* \cdot y_i$
  - If *isu* = 4, $s_i \leftarrow s_i - x_i^* \cdot y_i$
  - where $i = 1, n$
  - Specified as: a fullword integer. Its value must be 1, 2, 3, or 4.
- *x* is the vector (or matrix) *x*, containing the $x_i$ vectors of length *m*, used in the *n* dot product computations. Specified as: a one- or two-dimensional array of (at least) length $(1+(n-1)(*incx*o))+(*m*-1)*incx*i$, containing numbers of the data type indicated in Table 49 on page 225.
- *incx*_i is the stride for *x* in the inner loop—that is, the stride identifying the elements in each vector *x*_i. Specified as: a fullword integer. It can have any value.
- *incx*_o is the stride for *x* in the outer loop—that is, the stride identifying each vector *x*_i in *x*. Specified as: a fullword integer; *incx*_o ≥ 0.
- *y* is the vector (or matrix) *y*, containing the *y*_i vectors of length *m*, used in the *n* dot product computations. Specified as: a one- or two-dimensional array of (at least) length $(1+(n-1)(*incy*o)) + (m-1)*incy*i$, containing numbers of the data type indicated in Table 49 on page 225.
- *incy*_i is the stride for *y* in the inner loop—that is, the stride identifying the elements in each vector *y*_i. Specified as: a fullword integer. It can have any value.
- *incy*_o is the stride for *y* in the outer loop—that is, the stride identifying each vector *y*_i in *y*. Specified as: a fullword integer; *incy*_o ≥ 0.

### On Return

- *s* is the vector *s* of length *n*, containing the results of the *n* dot product computations. The type of dot product computation depends on the value specified for *isu*.
  - If *isu* = 1, $s_i = x_i^* \cdot y_i$
  - If *isu* = 2, $s_i = -x_i^* \cdot y_i$
  - If *isu* = 3, $s_i = s_i + x_i^* \cdot y_i$
  - If *isu* = 4, $s_i = s_i - x_i^* \cdot y_i$
  - where *i* = 1, *n*
  - Returned as: a one-dimensional array, containing numbers of the data type indicated in Table 49 on page 225.

### Function

The four possible computations that can be performed by these subprograms are:

- $s_i = x_i^* \cdot y_i$  Store positive dot product
- $s_i = -x_i^* \cdot y_i$  Store negative dot product
- $s_i = s_i + x_i^* \cdot y_i$  Accumulate positive dot product
- $s_i = s_i - x_i^* \cdot y_i$  Accumulate negative dot product
- for *i* = 1, *n*

where each *s*_i is a scalar element in the vector *s* of length *n*, and each of the *n* *x*_i and *y*_i vectors of length *m* are contained in vectors (or matrices) *x* and *y*, respectively. Each computation uses the dot product, which is expressed:

$$
x_i^* \cdot y_i = u_1v_1 + u_2v_2 + ... + u_mv_m
$$
