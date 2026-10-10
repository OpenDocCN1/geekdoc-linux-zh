# Error Conditions

Resource Errors:  Unable to allocate internal work area (CGEMUL and ZGEMUL only).

Computational Errors:  None

Input-Argument Errors:

+   1. $l da, l db, l dc \geq 0$
+   2. $l, m, n < 0$
+   3. $l > l dc$
+   4. $transa, transb \neq$ 'N' or 'T' for SGEMUL and DGEMUL
+   5. $transa, transb \neq$ 'N', 'T', or 'C' for CGEMUL and ZGEMUL
+   6. $transa =$ 'N' and $l > l da$
+   7. $transa =$ 'T' or 'C' and $m > l da$
+   8. $transb =$ 'N' and $m > l db$
+   9. $transb =$ 'T' or 'C' and $n > l db$

# Example 1

This example shows the computation $C \leftarrow AB$, where $A, B$, and $C$ are contained in larger arrays $A, B$, and $C$, respectively.

Call Statement and Input:

```
```text
             A      LDA   TRANSA       B      LDB    TRANSB       C      LDC   L      M      N
             |      |     |            |      |      |            |      |     |      |      |
CALL SGEMUL( A, 8, 'N' , B, 6, 'N' , C, 7, 6, 5, 4 )
```
```

![](bbox=[0.27, 0.48, 0.58, 0.6])

![](bbox=[0.27, 0.61, 0.58, 0.71])

Output:

![](bbox=[0.27, 0.75, 0.55, 0.85])

# Example 2

This example shows how to produce the transpose of the result of the computation performed in “Example 1,” $C \leftarrow AB$, which uses the calling sequence:

```
```text
CALL SGEMUL (A,8,'N',B,6,'N',C,7,6,5,4)
```
```