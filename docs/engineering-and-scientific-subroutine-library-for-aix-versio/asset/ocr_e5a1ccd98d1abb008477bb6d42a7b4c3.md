# SGEEV, DGEEV, CGEEV, and ZGEEV

```
SELECT = [
.TRUE.   
.FALSE.   
.TRUE.   
.TRUE.   
]
```

Output:

```
W = [
(0.999999,  0.000000)
(2.000001,  0.000000)
(2.999996,  0.000000)
(3.999999,  0.000000)
]
```

```
Z = [
(1.000000,  0.000000)   (-0.674014,  0.000000)   (-0.474306,  0.000000)
(0.750000,  0.000000)   (-0.674014,  0.000000)   (-0.474306,  0.000000)
(0.500000,  0.000000)   (-0.674013,  0.000000)   (-0.474306,  0.000000)
(0.250000,  0.000000)   (-0.337006,  0.000000)   (-0.474305,  0.000000)
]
```

# Example 5

This example shows how to find the eigenvalues and selected eigenvectors of a real short-precision general matrix $A$ of order 3, where:

+   * NAUX is equal to $\mathbb{N}^2+4\mathbb{N}$.
+   * AUX contains NAUX elements.
+   * The first and second eigenvectors are selected and appear in the first and second columns of matrix Z, respectively.
+   * On output, A has been overwritten.

**Note:** This matrix is used in Example 5.4 in referenced text [65].

# Call Statement and Input:

```
1OPT  A  LDA  W  Z  LDZ  SELECT  N  AUX  NAUX
 |    |    |    |    |     |     |   |
CALL SGEEV( 2,  A,  3,  W,  Z,  3,  SELECT,  3,  AUX, 21 )
```

```
A = [
 8.0  -1.0  -5.0
-4.0   4.0  -2.0
18.0  -5.0  -7.0
]
```

```
SELECT = [
.TRUE.
.TRUE.
.FALSE.
]
```

Output:

```
W = [
(1.999999,  3.999998)
(1.999999, -3.999998)
(0.999997,  0.000000)
]
```

```
Z = [
(0.500000,  0.000000)  (0.500000,  0.000000)
(0.500000,  0.500000)  (0.500000, -0.500000)
(0.500000, -0.500000)  (0.500000,  0.500000)
]
```