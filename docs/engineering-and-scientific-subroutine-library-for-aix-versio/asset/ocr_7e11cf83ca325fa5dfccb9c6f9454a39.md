# SAXPY, DAXPY, CAXPY, and ZAXPY

The computation is expressed as follows:

![](bbox=[0.28, 0.13, 0.52, 0.23])

See reference [81]. If alpha or n is zero, no computation is performed. For CAXPY, intermediate results are accumulated in long precision.

# Error Conditions

+   - Computational Errors: None

+   - Input-Argument Errors: $n<0$

# Example 1

This example shows vectors $x$ and $y$ with positive strides.

**Call Statement and Input:**

```
```
     N   ALPHA   X   INCX   Y   INCY
     |	|	|	|	|	|
CALL SAXPY( 5 , 2.0 , X , 1 , Y , 2  )
```
X = (1.0, 2.0, 3.0, 4.0, 5.0)
Y = (1.0, . , 1.0, . , 1.0, . , 1.0, . , 1.0)
```

**Output:**

```
```
     Y       = (3.0, . , 5.0, . , 7.0, . , 9.0, . , 11.0)
```
```

# Example 2

This example shows vectors $x$ and $y$ having strides of opposite signs. For $y$, which has negative stride, processing begins at element $Y(5)$, which is 1.0.

**Call Statement and Input:**

```
```
     N   ALPHA   X   INCX   Y   INCY
     |	|	|	|	|	|
CALL SAXPY( 5 , 2.0 , X , 1 , Y , -1 )
```
X = (1.0, 2.0, 3.0, 4.0, 5.0)
Y = (5.0, 4.0, 3.0, 2.0, 1.0)
```

**Output:**

```
```
     Y       = (15.0, 12.0, 9.0, 6.0, 3.0)
```
```

# Example 3

This example shows a vector, $x$, with 0 stride. Vector $x$ is treated like a vector of length $n$, all of whose elements are the same as the single element in $x$.

**Call Statement and Input:**