# STRMM, DTRMM, CTRMM, and ZTRMM

+   7. $diag \neq \text{'N'}$ or 'U'
+   8. $side = \text{'L'}$ and $m > lda$
+   9. $m > ldb$
+   10. $side = \text{'R'}$ and $n > lda$

# Example 1

This example shows the computation $B \leftarrow \alpha AB$, where $A$ is a 5 by 5 upper triangular matrix that is not unit triangular, and $B$ is a 5 by 3 rectangular matrix.

# Call Statement and Input:

```
SIDE UPLO TRANS DIAG M N ALPHA A LDA B LDB
| | | | | | | | | |
CALL STRMM( 'L' , 'U' , 'N' , 'N' , 5 , 3 , 1.0 , A , 7 , B , 6 )
```

A = \begin{bmatrix} 3.0 & -1.0 & 2.0 & 2.0 & 1.0 \\ . & -2.0 & 4.0 & -1.0 & 3.0 \\ . & . & -3.0 & 0.0 & 2.0 \\ . & . & . & 4.0 & -2.0 \\ . & . & . & . & 1.0 \\ . & . & . & . & . \end{bmatrix}

B = \begin{bmatrix} 2.0 & 3.0 & 1.0 \\ 5.0 & 5.0 & 4.0 \\ 0.0 & 1.0 & 2.0 \\ 3.0 & 1.0 & -3.0 \\ -1.0 & 2.0 & 1.0 \\ . & . & . \end{bmatrix}

Output:

B = \begin{bmatrix} 6.0 & 10.0 & -2.0 \\ -16.0 & -1.0 & 6.0 \\ -2.0 & 1.0 & -4.0 \\ 14.0 & 0.0 & -14.0 \\ -1.0 & 2.0 & 1.0 \\ . & . & . \end{bmatrix}

# Example 2

This example shows the computation $B \leftarrow \alpha A^{\mathrm{T}} B$, where $A$ is a 5 by 5 upper triangular matrix that is not unit triangular, and $B$ is a 5 by 4 rectangular matrix.

# Call Statement and Input:

```
SIDE UPLO TRANS DIAG M N ALPHA A LDA B LDB
| | | | | | | | | |
CALL STRMM( 'L' , 'U' , 'T' , 'N' , 5 , 4 , 1.0 , A , 7 , B , 6 )
```

A = \begin{bmatrix} -1.0 & -4.0 & -2.0 & 2.0 & 3.0 \\ . & -2.0 & 2.0 & 2.0 & 2.0 \\ . & . & -3.0 & -1.0 & 4.0 \\ . & . & . & 1.0 & 0.0 \\ . & . & . & . & -2.0 \\ . & . & . & . & . \end{bmatrix}

B = \begin{bmatrix} 1.0 & 2.0 & 3.0 & 4.0 \\ 3.0 & 3.0 & -1.0 & 2.0 \\ -2.0 & -1.0 & 0.0 & 1.0 \end{bmatrix}