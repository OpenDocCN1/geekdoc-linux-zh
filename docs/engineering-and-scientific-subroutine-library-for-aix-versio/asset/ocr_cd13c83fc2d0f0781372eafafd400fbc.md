# SGTHR, DGTHR, CGTHR, and ZGTHR

# Function

The copy is expressed as follows:

```
xᵢ ← y_IND₍ᵢ₎    for i = 1, nz
```

where:

+   *   **x** is a sparse vector, stored in compressed-vector storage mode.
+   *   **INDX** is the indices array for sparse vector **x**.
+   *   **y** is a sparse vector, stored in full-vector storage mode.

See reference [31]. If nz is 0, no copy is performed.

# Error Conditions

Computational Errors:  None

Input-Argument Errors:  *nz* < 0

# Example 1

This example shows how to use SGTHR to copy specified elements of a vector *y* into a sparse vector *x* of length 5, where the elements of array INDX are in ascending order.

Call Statement and Input:

```
NZ    Y    X    INDX
|     |     |     |
CALL SGTHR( 5 , Y , X , INDX )
```

```
Y     = (6.0, 2.0, 4.0, 7.0, 6.0, 10.0, -2.0, 8.0, 9.0, 0.0)
INDX  = (1, 3, 4, 7, 9)
```

Output:

```
X     = (6.0, 4.0, 7.0, -2.0, 9.0)
```

# Example 2

This example shows how to use SGTHR to copy specified elements of a vector *y* into a sparse vector *x* of length 5, where the elements of array INDX are in random order. (Note that the element 0.0 occurs in output vector *x*. This does not produce an error.)

Call Statement and Input:

```
NZ    Y    X    INDX
|     |     |     |
CALL SGTHR( 5 , Y , X , INDX )
```

```
Y     = (6.0, 2.0, 4.0, 7.0, 6.0, 10.0, -2.0, 8.0, 9.0, 0.0)
INDX  = (4, 3, 1, 10, 7)
```

Output:

```
X     = (7.0, 4.0, 6.0, 0.0, -2.0)
```

# Example 3

This example shows how to use CGTHR to copy specified elements of a vector, *y*, into a sparse vector, *x*, of length 3, where the elements of array INDX are in random order.

Call Statement and Input: