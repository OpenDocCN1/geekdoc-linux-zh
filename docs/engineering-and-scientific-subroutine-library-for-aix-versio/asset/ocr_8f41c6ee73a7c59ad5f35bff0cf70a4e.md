![](bbox=[0.33, 0.08, 0.52, 0.14])

# Example 4

This example shows how to factor the first six rows and columns, referred to as matrix $AI$, of the 9 by 9 general sparse matrix $A$ from Example 1 and compute the determinant of $AI$. Input matrix $AI$, shown here, is stored in diagonal-out skyline storage mode. Input matrix $AI$ is:

![](bbox=[0.43, 0.24, 0.68, 0.31])

Output matrix $AI$, shown here, is in $LU$ factored form with $U^{-1}$ on the diagonal, and is stored in diagonal-out skyline storage mode. Output matrix $AI$ is:

![](bbox=[0.43, 0.39, 0.68, 0.46])

Call Statement and Input:

![](bbox=[0.28, 0.5, 0.9, 0.53])

+   - AU = (same as input AU in Example 1)
+   - IDU = (1, 2, 4, 7, 10, 14, 17)
+   - AL = (same as input AL in Example 1)
+   - IDL = (1, 2, 4, 7, 11, 13, 18)
+   - IPARM = (1, 11, 0, 0, 0, ..., ..., 0, ... , ..., ...)
+   - RPARM = (not relevant)
+   - BX = (not relevant)
+   - LDBX = (not relevant)
+   - MBX = (not relevant)

Output:

+   - AU = (0.5, 0.5, 2.0, 0.5, 2.0, 2.0, 0.5, 2.0, 2.0, 0.5, 2.0, 2.0, 0.5, 2.0, 2.0, 8.0, 8.0, 4.0, 4.0, 2.0, 8.0, 6.0, 4.0, 2.0, 16.0, 10.0, 8.0, 10.0, 4.0, 6.0, 4.0, 2.0)
+   - IDU = (same as input)
+   - AL = (0.0, 0.0, 1.0, 0.0, 1.0, 1.0, 0.0, 1.0, 1.0, 1.0, 0.0, 1.0, 0.0, 1.0, 1.0, 1.0, 0.0, 6.0, 4.0, 2.0, 0.0, 8.0, 6.0, 4.0, 2.0, 0.0, 8.0, 10.0, 6.0, 8.0, 6.0, 6.0, 4.0, 2.0)
+   - IDL = (same as input)
+   - IPARM = (1, 11, 0, 0, 0, ..., ..., ..., 0, ..., ..., ..., 3,