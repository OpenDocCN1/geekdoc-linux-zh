SPOTRF, DPOTRF, CPOTRF, ZPOTRF, SPOF, DPOF, CPOF, ZPOF, SPTRF, DPTRF, SPF, and DPFF

```
A = [ (25.0,  . )
      (-5.0,  5.0) (51.0,  .  )
      (10.0,  -5.0) ( 4.0,  6.0) (71.0,  .  ) ]
```

# Output:

```
A = [ ( 5.0,  0.0)
      (-1.0,  1.0) ( 7.0,  0.0)
      ( 2.0,  -1.0) ( 1.0,  1.0) (8.0,  0.0) ]
```

```
INFO = 0
```

# Example 4

This example shows a factorization of positive definite complex Hermitian matrix A of order 3, stored in upper storage mode, where on input matrix A is:

```
A = [ (9.0,  0.0) (3.0,  3.0) (3.0,  -3.0)
      (3.0,  -3.0) (18.0,  0.0) (8.0,  -6.0)
      (3.0,    3.0) (8.0,  6.0) (43.0,   0.0) ]
```

Note: On input, the imaginary parts of the diagonal elements of the complex Hermitian matrix A are assumed to be zero, so you do not have to set these values. On output, they are set to zero.

# Call Statement and Input:

```
UPLO  N   A    LDA    INFO
  |    |   |     |      |
CALL CPOTRF( 'U' , 3 , A , 3 , INFO )
or
UPLO   A   LDA     N
  |    |    |      |
CALL CPOF( 'U' , A , 3 , 3 )
```

```
A = [ (9.0,   .  ) (3.0,3.0) ( 3.0,-3.0)
      ( . ,    .  ) (18.0,  .) ( 8.0,-6.0)
      ( . ,    .  ) ( . ,    .) (43.0,   .  ) ]
```

# Output:

```
A = [ (3.0,  0.0)  (1.0,  1.0) (1.0,  -1.0)
      ( . ,    .  )  (4.0,  0.0) (2.0,  -1.0)
      ( . ,    .  )  ( . ,    .  ) (6.0,   0.0) ]
```

```
INFO = 0
```

# Example 5

This example shows a factorization (using the Cholesky factorization method) of the same positive definite symmetric matrix A of order 9 used in "Example 7" on page 486, but stored in upper-packed storage mode.

Note: The AP arrays are formatted in a triangular arrangement for readability; however, they are stored in upper-packed storage mode.

# Call Statement and Input: