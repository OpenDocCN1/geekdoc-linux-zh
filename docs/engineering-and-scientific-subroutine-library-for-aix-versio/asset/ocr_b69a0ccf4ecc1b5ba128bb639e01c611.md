# DGELS

# **Example 2**

This example finds the minimum norm solution of an underdetermined system $A^{T}X = B$. Matrix $A$ is size $6 	imes 2$. On input, matrix $B$ is size $2 	imes 1$, stored in array $b$ with leading dimension 6.

**Note:** Because $lwork = 0$, DGELS dynamically allocates the work area used by this subroutine.

# **Call Statements and Input:**

```
TRANSAMNLRDSAIDABLDNWOKLWORKINLO
|
|
|
|
|
|
|
|
|
|
CALLDGELS('T') , 6 , 2 ,1 , A , 6 ,B , 6 , WORK , 0 , INFO)
```

General matrix $A$ of size $6 	imes 2$:

$$
A 
 = 
 \begin{bmatrix}
 .000000000 & 2.000000000 \
 2.000000000 & -1.000000000 \
 2.000000000 & -1.000000000 \
 .000000000 & 1.500000000 \
 2.000000000 & -1.000000000 \
 2.000000000 & -1.000000000
 \end{bmatrix}
$$

General matrix $B$ of size $2 	imes 1$:

$$
B 
 = 
 \begin{bmatrix}
 1.000000000 \
 1.000000000
 \end{bmatrix}
$$

# **Output:**

General matrix $A$ is overwritten.

Solution matrix $X$ overwrites $B$:

$$
B 
 = 
 \begin{bmatrix}
 .480000000 \
 .125000000 \
 .125000000 \
 .360000000 \
 .125000000 \
 .125000000
 \end{bmatrix}
$$

```
INFO 
 = 
 0
```

# **Example 3**

This example finds the minimum norm solution of an underdetermined system $AX = B$. Matrix $A$ is size $3 	imes 4$. On input, matrix $B$ is size $3 	imes 4$, stored in array $b$ with leading dimension 4.

**Note:** Because $lwork = 0$, DGELS dynamically allocates the work area used by this subroutine.

# **Call Statements and Input:**

```
TRANSAMNLRDSAIDABLDNWOKLWORKINLO
|
|
|
|
|
|
|
|
|
|
CALLDGELS('N') , 3 , 4 , 4 , A , 3 , B , 4 , WORK , 0 , INFO)
```

General matrix $A$ of size $3 	imes 4$: