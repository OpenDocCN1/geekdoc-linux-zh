# SGEADD, DGEADD, CGEADD, and ZGEADD

```
c_{ij} = a_{ij} + b_{ji} \text{ for } C\leftarrow A^T + B^T
\text{for } i=1, m \text{ and } j=1, n
```

If $m$ or $n$ is 0, no computation is performed.

Special Usage

You can compute the transpose $C^T$ of each of the four computations listed under “Function” on page 366 by using the following matrix identities:

```
(A + B)^T = A^T + B^T
(A + B^T)^T = A^T + B
(A^T + B)^T = A + B^T
(A^T + B^T)^T = A + B
```

Be careful that your output array receiving $C^T$ has dimensions large enough to hold the transposed matrix. See “Example 4” on page 369.

# Error Conditions

Computational Errors: None

Input-Argument Errors:

+   1. lda, ldb, ldc <= 0
+   2. m, n < 0
+   3. m > ldc
+   4. transa, transb != 'N' or 'T'
+   5. transa = 'N' and m > lda
+   6. transa = 'T' and n > lda
+   7. transb = 'N' and m > ldb
+   8. transb = 'T' and n > ldb

# Example 1

This example shows the computation C←A+B, where A and C are contained in larger arrays A and C, respectively, and B is the same size as array B, in which it is contained.

Call Statement and Input:

```
A   LDA   TRANS   B   LDB   TRANS   C   LDC   M   N
    |       |       |         |         |       |   |     |
CALL SGEADD( A , 6 , 'N' , B , 4 , 'N' , C , 5 , 4 , 3 )
```

```
A    = \begin{bmatrix} 110000.0 & 120000.0 & 130000.0 \\ 210000.0 & 220000.0 & 230000.0 \\ 310000.0 & 320000.0 & 330000.0 \\ 410000.0 & 420000.0 & 430000.0 \\ \vdots & \vdots & \vdots \end{bmatrix}
B    = \begin{bmatrix} 11.0 & 12.0 & 13.0 \\ 21.0 & 22.0 & 23.0 \\ 31.0 & 32.0 & 33.0 \\ 41.0 & 42.0 & 43.0 \end{bmatrix}
```

Output:

```
\begin{bmatrix} 110011.0 & 120012.0 & 130013.0 \\ 210021.0 & 220022.0 & 230023.0 \end{bmatrix}
```