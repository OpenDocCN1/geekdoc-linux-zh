# SGESVF and DGESVF

B = [7.0 10.0; 8.0 11.0; 9.0 12.0]

Output:

A = [0.922 -0.386; -0.386 -0.922; . .]

B = [-1.310 -2.321; -13.867 -18.963; . .]

X = (0.773, 9.508)

# Example 5

This example computes the singular values, s, and matrices $V$ and $U^{T}B$ in preparation for solving the overdetermined system $AX=B$. The singular values are sorted in descending order, and the columns of $V$ and the rows of $U^{T}B$ are swapped to correspond to the sorted singular values.

+   - M is greater than N.
+   - Naux is greater than or equal to $2N + \max(M, N, NB) = 7$.
+   - The singular values are returned in S.
+   - The matrix V is returned in A.
+   - The matrix $U^{T}B$ is returned in B.

# Call Statement and Input:

```
```
 I OPT A L DA B LDB NB S M N AUX NAUX
CALL DGESVF( 12 , A , 3 , B , 3 , 2 , S , 3 , 2 , AUX , 7 )
```

A = [1.0 4.0; 2.0 5.0; 3.0 6.0]

B = [7.0 10.0; 8.0 11.0; 9.0 12.0]
```

Output:

A = [-0.386 0.922; -0.922 -0.386; . .]

B = [-13.867 -18.963; -1.310 -2.321; . .]

S = (9.508, 0.773)