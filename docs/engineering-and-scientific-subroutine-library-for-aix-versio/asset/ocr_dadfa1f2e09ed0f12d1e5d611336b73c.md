# SGETMO, DGGETMO, CGGETMO, and ZGETMO

# Function

Matrix $A$ is transposed out of place; that is, the $m$ rows and $n$ columns in matrix $A$ are stored in $n$ rows and $m$ columns of matrix $B$. For matrix $A$ with elements $a_{ij}$, where $i = 1, m$ and $j = 1, n$, the out-of-place transpose is expressed as $b_{ji} = a_{ij}$ for $i = 1, m$ and $j = 1, n$.

For the following input matrix $A$:

![](bbox=[0.28, 0.2, 0.47, 0.33])

the out-of-place matrix transpose operation $B \leftarrow A^{T}$ is expressed as:

![](bbox=[0.28, 0.37, 0.55, 0.47])

If $m$ or $n$ is 0, no computation is performed.

# Error Conditions

Computational Errors: None

# Input-Argument Errors:

+   1. $m < 0$ or $m > lda$
+   2. $n < 0$ or $n > ldb$
+   3. $lda \leq 0$
+   4. $ldb \leq 0$

# Example 1

This example shows an out-of-place matrix transpose of matrix $A$, having 5 rows and 4 columns, with the result going into matrix $B$.

# Call Statement and Input:

```
CALL SGETMO( A(2,3) , 10 , 5 , 4 , B(2,2) , 6 )
```

![](bbox=[0.28, 0.77, 0.58, 0.91])