![](bbox=[0.28, 0.08, 0.46, 0.18])

See reference [81]. If $n$ is 0, no computation is performed. For CSCAL, intermediate results are accumulated in long precision.

# Error Conditions

Computational Errors: None

Input-Argument Errors: $n<0$ 

# Example 1

This example shows a vector, $x$, with a stride of 1.

Call Statement and Input:

N ALPHA X INCX

```
CALL SSCAL( 5 , 2.0 , X , 1 )
```

```
X = (1.0, 2.0, 3.0, 4.0, 5.0)
```

Output:

```
X = (2.0, 4.0, 6.0, 8.0, 10.0)
```

# Example 2

This example shows vector, $x$, with a stride greater than 1.

Call Statement and Input:

N ALPHA X INCX

```
CALL SSCAL( 5 , 2.0 , X , 2 )
```

```
X = (1.0, ., 2.0, ., 3.0, ., 4.0, ., 5.0)
```

Output:

```
X = (2.0, ., 4.0, ., 6.0, ., 8.0, ., 10.0)
```

# Example 3

This example illustrates that when the strides for two similar computations (Example 1 and Example 3) have the same absolute value but have opposite signs, the output is the same. This example is the same as Example 1, except the stride for $x$ is negative (−1). For performance reasons, it is better to specify the positive stride. For $x$, processing begins at element $X(5)$, which is $5.0$, and results are stored beginning at the same element.

Call Statement and Input:

N ALPHA X INCX

```
CALL SSCAL( 5 , 2.0 , X , -1 )
```

```
X = (1.0, 2.0, 3.0, 4.0, 5.0)
```

Output: