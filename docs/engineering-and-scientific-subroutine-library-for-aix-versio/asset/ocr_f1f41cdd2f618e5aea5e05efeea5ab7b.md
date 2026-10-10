# ## SGETMI, DGETMI, CGETMI, and ZGETMI—General Matrix Transpose (In-Place)

These subroutines transpose an $n$ by $n$ matrix $A$ in place—that is, in matrix $A$:
$A \leftarrow A^{T}$

**Table 85. Data Types**

| A | Subroutine |
|---|---|
| Short-precision real | SGETMI |
| Long-precision real | DGETMI |
| Short-precision complex | CGETMI |
| Long-precision complex | ZGETMI |

# **Syntax**

| Fortran | CALL SGETMI \| DGETMI \| CGETMI \| ZGETMI ($a$, $lda$, $n$) |
| C and C++ | sgetmi \| dgetmi \| cgetmi \| zgetmi ($a$, $lda$, $n$); |

**On Entry:**

*   $a$ is the matrix $A$ having $n$ rows and $n$ columns.
    *   Specified as: an $lda$ by (at least) $n$ array, containing numbers of the data type indicated in Table 85.
*   $lda$ is the leading dimension of the array specified for $a$.
    *   Specified as: a fullword integer; $lda > 0$ and $lda \geq n$.
*   $n$ is the number of rows and columns in matrix $A$.
    *   Specified as: a fullword integer; $n \geq 0$.

**On Return:**

*   $a$ is the $n$ by $n$ matrix $A^{T}$, containing the results of the matrix transpose operation. Returned as: an $lda$ by (at least) $n$ array, containing numbers of the data type indicated in Table 85.

+   **Notes**
+   
+   1. To achieve optimal performance in these subroutines, specify an even value for $lda$. An odd value may degrade performance.
+   2. To achieve optimal performance in CGETMI, align the array specified for $a$ on a doubleword boundary.

**Function**
Matrix $A$ is transposed in place; that is, the $n$ rows and $n$ columns in matrix $A$ are exchanged. For matrix $A$ with elements $a_{ij}$ where $i, j = 1, n$, the in-place transpose is expressed as $a_{ji} = a_{ij}$ for $i, j = 1, n$.

For the following input matrix $A$: