# STRSM, DTRSM, CTRSM, and ZTRSM

# Example 6

This example shows the solution *B*α(*A*⁻¹*H*B*, where *A* is a complex 5 by 5 upper triangular matrix that is not unit triangular, and *B* is a complex 5 by 1 rectangular matrix.

# Call Statement and Input:

```
CALL CTRSM('L', 'U', 'C', 'N', 5, 1, ALPHA, A, 6, B, 6)
ALPHA = (1.0, 0.0)
```

A = [(-4.0, 1.0)  (4.0, -3.0)  (-1.0, 3.0)  (0.0, 0.0)  (-1.0, 0.0)]
    [      .        (-2.0, 0.0) (-3.0, -1.0) (-2.0, -1.0)  (4.0, 3.0)]
    [      .           .         (-5.0, 3.0)  (-3.0, -3.0)  (-5.0, -5.0)]
    [      .           .           .           (4.0, -4.0)   (2.0, 0.0)]
    [      .           .           .           .             (2.0, -1.0)]

B = [(-8.0, -19.0)]
    [( 8.0, 21.0)]
    [(44.0, -8.0)]
    [(13.0, -7.0)]
    [(19.0, 2.0)]
    [      .]

# Output:

B = [(3.0, 4.0)]
    [(-4.0, 2.0)]
    [(-5.0, 0.0)]
    [(1.0, 3.0)]
    [(3.0, 1.0)]
    [      .]