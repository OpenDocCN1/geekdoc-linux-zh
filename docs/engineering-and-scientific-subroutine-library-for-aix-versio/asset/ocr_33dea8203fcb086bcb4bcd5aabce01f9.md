and on output, matrix A is:

```
[ 1.0  1.0  1.0  0.0  0.0  0.0  0.0  0.0  0.0]
[ 1.0  1.0  1.0  1.0  0.0  0.0  0.0  0.0  0.0]
[ 1.0  1.0  1.0  1.0  1.0  0.0  0.0  0.0  0.0]
[ 0.0  1.0  2.0  1.0  1.0  0.0  0.0  0.0  0.0]
[ 0.0  0.0  0.0  0.0  1.0  1.0  1.0  1.0  0.0]
[ 0.0  0.0  0.0  0.0  0.0  1.0  1.0  1.0  1.0]
[ 0.0  0.0  0.0  0.0  0.0  0.0  1.0  1.0  1.0]
[ 0.0  0.0  0.0  0.0  0.0  0.0  0.0  1.0  1.0]
```

where array location APB(2,9) is set to 0.0.

# **Call Statement and Input:**

```
APB LDA N M
CALL SPBF( APB , 3 , 9 , 2 )
```

```
APB = [ 1.0  2.0  3.0  3.0  3.0  3.0  3.0  3.0  3.0
         1.0  2.0  2.0  2.0  2.0  2.0  2.0  2.0  .
         1.0  1.0  1.0  1.0  1.0  1.0  1.0  .  . ]
```

# **Output:**

```
APB = [ 1.0  1.0  1.0  1.0  1.0  1.0  1.0  1.0  1.0
         1.0  1.0  1.0  1.0  1.0  1.0  1.0  1.0  0.0
         1.0  1.0  1.0  1.0  1.0  1.0  1.0  .  . ]
```

# **Example 2**

This example shows a Cholesky factorization of the same matrix used in Example 1.

# **Call Statement and Input:**

```
APB LDA N M
CALL SPCCHF( APB , 3 , 9 , 2 )
```

```
APB = (same as input APB in Example 1)
```

# **Output:**

```
APB = [ 1.0  1.0  1.0  1.0  1.0  1.0  1.0  1.0  1.0
         1.0  1.0  1.0  1.0  1.0  1.0  1.0  .  .
         1.0  1.0  1.0  1.0  1.0  1.0  1.0  .  . ]
```