# SWLEV, DWLEV, CWLEV, and ZWLEV

# Example 2

This example shows how to compute filter coefficients in vector **y** by solving the system $Ay = u$. Matrix $A$ is:

![](bbox=[0.45, 0.15, 0.64, 0.21])

This input Toeplitz matrix is not positive definite, as indicated by the zero value in $AUX(1)$ on output.

# Call Statement and Input:

```
CALL SWLEV( X , 1 , 0 , 1 , Y , 1 , 4 , AUX , 12 )
```

X = (10.0, -8.0, 7.0, -5.0)

U = (40.0, -10.0, 30.0, 20.0)

AUX = (not relevant)

# Output:

Y = (5.1111, 5.5555, 12.2222, 10.4444)

AUX = (0.0, . , . , . , . , . , . , . , . , . , . , . , . , . , . , .)

# Example 3

This example shows a vector $x$ with a stride greater than 1, a vector $u$ with a negative stride, and a vector $y$ with a stride of 1. It uses the same input Toeplitz matrix as in Example 2, which is not positive definite.

# Call Statement and Input:

```
CALL SWLEV( X , 2 , 0 , -2 , Y , 1 , 4 , AUX , 12 )
```

X = (10.0, , -8.0, , 7.0, , -5.0)

U = (20.0, , 30.0, , -10.0, , , 40.0)

AUX = (not relevant)

# Output:

Y = (5.1111, 5.5555, 12.2222, 10.4444)

AUX = (0.0, . , . , . , . , . , . , . , . , . , . , . , . , . , . , .)

# Example 4

This example shows how to compute filter coefficients in vector **y** by solving the system $Ay = u$. Matrix $A$ is:

![](bbox=[0.35, 0.79, 0.76, 0.85])

This input complex Hermitian Toeplitz matrix is positive definite, as indicated by the zero value in $AUX(1)$ on output.

# Call Statement and Input: