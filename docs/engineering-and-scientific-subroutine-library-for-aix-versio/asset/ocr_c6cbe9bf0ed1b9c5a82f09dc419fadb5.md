# Example 4

This example shows how to use SGBMV to perform the computation $y \leftarrow \beta y + \alpha A x$, where $m l \geq m$ and $m u \geq n$, TRANSA is equal to 'N', and the following real general band matrix $A$ is used in the computation. Matrix $A$ is:

```
```
     1.0  1.0  1.0  1.0  1.0
     2.0  2.0  2.0  2.0  2.0
     3.0  3.0  3.0  3.0  3.0
     4.0  4.0  4.0  4.0  4.0
```
```

# Call Statement and Input:

```
```
      TRANSA  M    N    ML   MU   ALPHA  A    LDA    X   INCX  BETA   Y    INCY

CALL SGBMV ( 'N' , 4  , 5  , 6  , 5  ,  2.0  , A , 12 , X , 1  , 10.0 , Y , 2  )
```
```

```
```
A  =  [   .   .   .   .   .
          .   .   .       1.0
          .   .   .   1.0  2.0
          .   1.0  2.0  3.0
          1.0  2.0  3.0  4.0  .
          1.0  2.0  3.0  4.0  .
          2.0  3.0  4.0  .   .
          3.0  4.0  .   .   .
          4.0  .   .   .   .
          .   .   .   .   .
          .   .   .   .   .
          .   .   .   .   .
          .   .   .   .   .   ]
```
```

```
```
X      =  (1.0, 2.0, 3.0, 4.0, 5.0)
Y      =  (1.0, . , 2.0, . , 3.0, . , 4.0, . )
```
```

# Output:

```
```
Y      =  (40.0, . , 80.0, . , 120.0, . , 160.0, . )
```
```