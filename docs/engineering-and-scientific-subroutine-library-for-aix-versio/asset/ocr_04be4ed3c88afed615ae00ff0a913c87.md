# SSEV, DSPEV, CHPEV, and ZHPEV

```
I OPT AP W Z LDZ N AUZ NAUX
CALL SSEV(0, AP, W, DUMMY, 1, 3, AUX, 3)

AP = (1.0, -1.0, 0.0, 2.0, -1.0, 1.0)
```

**Output:**

```
W = \[
0.000000 \\
1.000000 \\
3.000000
\]
```

# Example 2

This example shows how to find the eigenvalues and eigenvectors of a real short-precision symmetric matrix $A$ of order 4, stored in upper-packed storage mode. Matrix $A$ is:

```
\[
5.0 & 4.0 & 1.0 & 1.0 \\
4.0 & 5.0 & 1.0 & 1.0 \\
1.0 & 1.0 & 4.0 & 2.0 \\
1.0 & 1.0 & 2.0 & 4.0
\]
```

where:

+   - NAUX is equal to $2N$.
+   - AUX contains $2N$ elements.

**Note:** This matrix is used in Example 4.1 in referenced text [65].

**Call Statement and Input:**

```
I OPT AP W Z LDZ N AUZ NAUX
CALL SSEV(21, AP, W, Z, 4, 4, AUX, 8)

AP = (5.0, 4.0, 5.0, 1.0, 1.0, 4.0, 1.0, 1.0, 2.0, 4.0)
```

**Output:**

```
W = \[
1.000000 \\
2.000000 \\
5.000000 \\
9.999999
\]

Z = \[
0.707107 & 0.000000 & 0.316227 & 0.632455 \\
-0.707107 & 0.000000 & 0.316228 & 0.632455 \\
0.000000 & -0.707106 & -0.632455 & 0.316227 \\
0.000000 & 0.707107 & -0.632455 & 0.316228
\]
```

# Example 3

This example shows how to find the eigenvalues and eigenvectors of a real short-precision symmetric matrix $A$, stored in lower-packed storage mode, which has an eigenvalue of multiplicity 2. Matrix $A$ is:

```
\[
6.0 & 4.0 & 4.0 & 1.0 \\
4.0 & 6.0 & 1.0 & 4.0 \\
4.0 & 1.0 & 6.0 & 4.0 \\
1.0 & 4.0 & 4.0 & 6.0
\]
```