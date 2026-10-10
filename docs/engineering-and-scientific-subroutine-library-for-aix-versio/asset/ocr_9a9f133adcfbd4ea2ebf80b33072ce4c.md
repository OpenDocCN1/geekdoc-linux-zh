# **Example 4**

This example shows how to produce the transpose of the result of the computation performed in “Example 3” on page 368, $\mathit{C_{\alpha}+A^{\mathrm{T}}B^T}$, which uses the calling sequence:

```
CALL SGEADD( A , 5 , 'N' , B , 3 , 'T' , C , 4 , 4 , 3 )
```

You instead code a calling sequence for $\mathit{C^T+A^T+B}$, as shown below, where the resulting matrix $\mathit{C^T}$ in the output array $\mathit{CT}$ is the transpose of the matrix in the output array $\mathit{C}$ in Example 3. Note that the array $\mathit{CT}$ has dimensions large enough to receive the transposed matrix. For a description of all the matrix identities, see “Special Usage” on page 367.

# Call Statement and Input:

```
```
          A    LDA  TRANS   B    LDB  TRANS    C    LDC    M    N
         |      |     |      |      |     |      |      |     |    |
CALL SGEADD( A , 5 , 'T' , B , 3 , 'N' , CT , 4 , 3 , 4 )
```
```

![](bbox=[0.28, 0.32, 0.58, 0.4])

![](bbox=[0.28, 0.41, 0.54, 0.46])

# Output:

![](bbox=[0.28, 0.51, 0.65, 0.58])

# **Example 5**

This example shows the computation $\mathit{C_{\alpha}+A^{\mathrm{T}}B^T}$, where $\mathit{A, B,}$ and $\mathit{C}$ are the same size as the arrays $\mathit{A, B,}$ and $\mathit{C,}$ in which they are contained.

# Call Statement and Input:

```
```
          A    LDA  TRANS   B    LDB  TRANS    C    LDC    M    N
         |      |     |      |      |     |      |      |     |    |
CALL SGEADD( A , 3 , 'T' , B , 3 , 'T' , C , 4 , 4 , 3 )
```
```

![](bbox=[0.28, 0.71, 0.64, 0.77])

![](bbox=[0.28, 0.78, 0.54, 0.83])

# Output: