If *n* is 0, no computation is performed; if *nd* is 0, output vector *y* is set to zero, because matrix *A* contains all zeros.

# ### Error Conditions

**Computational Errors:**  None

+   **Input-Argument Errors:**
+   1.  *iopt* \( \neq \) 0 or 1
+   2.  *n* < 0
+   3.  *lda* \( \leq \) 0
+   4.  *n* > *lda*
+   5.  *trans* \( \neq \) 'N' or 'T'
+   6.  *nd* < 0
+   7.  LA(*j*) \( \leq \) - *n* or LA(*j*) \( \geq \) *n*, for any *j* = 1, *n*

# **Example 1**

This example shows the matrix-vector product using *trans* = 'N', which is computed for the following sparse matrix *A* of order 6. The matrix is stored in compressed-matrix storage mode in arrays AD and LA using the storage variation for general sparse matrices, storing all nonzero diagonals. Matrix *A* is:

![](bbox=[0.45, 0.4, 0.66, 0.49])

**Call Statement and Input:**

```
```
            IOPT   N   ND   AD LDA TRANS      LA X   Y
             |     |    |    |     |          |  |   |
CALL DSMX(  0   , 6  , 5  , AD ,  6 , 'N' , LA, X , Y )
```
```

```
```fortran
AD      =     [ 4.0  0.0  0.0  0.0  7.0
              4.0  0.0  0.0  3.0  2.0
              4.0  0.0  0.0  2.0  4.0
              4.0  0.0  0.0  7.0  1.0
              4.0  0.0  1.0  3.0  0.0
              4.0  1.0  1.0  3.0  0.0]
LA      =     (0, -5, -4, -1, 2)
X       =     (1.0, 2.0, 3.0, 4.0, 5.0, 6.0)
```
```

**Output:**
Y     =     (25.0, 19.0, 36.0, 43.0, 33.0, 42.0)

# **Example 2**

This example shows the matrix-vector product using *trans* = 'N', which is computed for the following sparse matrix *A* of order 6. The matrix is stored in compressed-matrix storage mode in arrays AD and LA using the storage variation for symmetric sparse matrices, storing the nonzero main diagonal and one of the unique nonzero diagonals. Matrix *A* is:

![](bbox=[0.42, 0.86, 0.69, 0.915])