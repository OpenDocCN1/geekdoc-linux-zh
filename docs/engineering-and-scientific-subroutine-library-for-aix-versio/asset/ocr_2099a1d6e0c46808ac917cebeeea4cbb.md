$X = \begin{bmatrix} -0.600 \\ -1.200 \\ 2.000 \end{bmatrix}$

# Example 2

This example finds the linear least squares solution for the overdetermined system $AX=B$, using the singular value decomposition computed by DGESVF. Matrix $A$ is:

![](bbox=[0.48, 0.21, 0.58, 0.27])

and where $B$ is:

![](bbox=[0.48, 0.31, 0.58, 0.37])

On output, matrix $U^TB$ is overwritten.

Note: This example corresponds to Example 4 of DGESVF on page 680.

# Call Statement:

```
CALL DGESV( V, 3, UB, 3, 2, S, X, 2, 3, 2, TAU )
```

# Input:

$V = \begin{bmatrix} 0.922 & -0.386 \\ -0.386 & -0.922 \\ . & . \end{bmatrix}$

$UB = \begin{bmatrix} -1.310 & -2.321 \\ -13.867 & -18.963 \\ . & . \end{bmatrix}$

$S = (0.773, 9.508)$
$TAU = 0.5171D-14$

# Output:

$X = \begin{bmatrix} -1.000 & -2.000 \\ 2.000 & 3.000 \end{bmatrix}$