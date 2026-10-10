# SAXPYI, DAXPYI, CAXPYI, and ZAXPYI

# Notes

+   1. Each value specified in array `INDX` must be unique; otherwise, results are unpredictable.
+   2. Vectors *x* and *y* must have no common elements; otherwise, results are unpredictable. See “Concepts” on page 55.
+   3. For a description of how sparse vectors are stored, see “Sparse Vector” on page 60.

# Function

The computation is expressed as follows:

```
$y_{\text{INDX}(i)} \leftarrow y_{\text{INDX}(i)} + \alpha x_{i}$ for $i = 1, nz$
```

where:

* *x* is a sparse vector, stored in compressed-vector storage mode.
* `INDX` is the indices array for sparse vector *x*.
* *y* is a sparse vector, stored in full-vector storage mode.

See reference [31]. If *α* or *nz* is zero, no computation is performed. For SAXPYI and CAXPYI, intermediate results are accumulated in long-precision.

# Error Conditions

**Computational Errors:** None

**Input-Argument Errors:** $nz < 0$

# Example 1

This example shows how to use SAXPYI to perform a computation using a sparse vector *x* of length 5, where the elements of array `INDX` are in ascending order.

# Call Statement and Input:

```
```
        NZ ALPHA X INDX Y
        |   |     |   |
CALL SAXPYI ( 5 , 2.0 , X , INDX , Y )

X       = (1.0, 2.0, 3.0, 4.0, 5.0)
INDX    = (1, 3, 4, 7, 10)
Y       = (1.0, 5.0, 4.0, 3.0, 6.0, 10.0, -2.0, 8.0, 9.0, 0.0)
```
```

**Output:**

```
```
Y       = (3.0, 5.0, 8.0, 9.0, 6.0, 10.0, 6.0, 8.0, 9.0, 10.0)
```
```

# Example 2

This example shows how to use SAXPYI to perform a computation using a sparse vector *x* of length 5, where the elements of array `INDX` are in random order.

# Call Statement and Input:

```
```
        NZ ALPHA X INDX Y
        |   |     |   |
CALL SAXPYI ( 5 , 2.0 , X , INDX , Y )

X       = (1.0, 2.0, 3.0, 4.0, 5.0)
INDX    = (4, 3, 1, 10, 7)
Y       = (1.0, 5.0, 4.0, 3.0, 6.0, 10.0, -2.0, 8.0, 9.0, 0.0)
```
```

**Output:**

```
```
Y       = (7.0, 5.0, 8.0, 5.0, 6.0, 10.0, 8.0, 8.0, 9.0, 8.0)
```
```