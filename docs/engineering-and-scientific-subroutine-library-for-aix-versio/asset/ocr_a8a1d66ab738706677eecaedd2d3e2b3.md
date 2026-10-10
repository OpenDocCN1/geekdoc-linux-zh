SYAX, DYAX, CYAX, ZYAX, CSYAX, ZDYAX

```
Y = {2.0, 2.0, 2.0, 2.0, 2.0}
```

# Example 4

This example shows how SYAX can be used to compute a scalar value. In this case both vectors x and y contain scalar values, and the strides for both vectors are 0. The number of elements to be processed, $n$, is 1.

# Call Statement and Input:

```
N   ALPHA X   INCX Y   INCY
1   |       |       |       |       |
CALL SYAX( 1, 2.0, X, 0, Y, 0 )
```

```
X = {1.0}
```

# Output:

```
Y = {2.0}
```

# Example 5

This example shows a scalar, $\alpha$, and vectors x and y, containing complex numbers, where both vectors have a stride of 1.

# Call Statement and Input:

```
N   ALPHA X   INCX Y   INCY
3   |       |       |       |       |
CALL CYAX( 3, ALPHA, X, 1, Y, 1 )
```

```
ALPHA = {2.0, 3.0}
X     = {{1.0, 2.0}, {2.0, 0.0}, {3.0, 5.0}}
```

# Output:

```
Y = {{-4.0, 7.0}, {4.0, 6.0}, {-9.0, 19.0}}
```

# Example 6

This example shows a scalar, $\alpha$, containing a real number, and vectors x and y, containing complex numbers, where both vectors have a stride of 1.

# Call Statement and Input:

```
N   ALPHA X   INCX Y   INCY
3   |       |       |       |       |
CALL CSYAX( 3, 2.0, X, 1, Y, 1 )
```

```
X = {{1.0, 2.0}, {2.0, 0.0}, {3.0, 5.0}}
```

# Output:

```
Y = {{2.0, 4.0}, {4.0, 0.0}, {6.0, 10.0}}
```