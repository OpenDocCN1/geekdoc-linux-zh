$\boldsymbol{v}_{i+1:m}$ is stored on return in $\boldsymbol{A}_{i+1:m, \ i}$

$\boldsymbol{I}$ is the identity matrix

For $m \geq n$, $\boldsymbol{R}$ is an upper triangular matrix.

For $m < n$, $\boldsymbol{R}$ is an upper trapezoidal matrix.

If $m = 0$ or $n = 0$, no computation is performed and the subroutine returns after doing some parameter checking.

See references [54,8,67,52,53].

# ## Error Conditions

**Resource Errors:** $l\mathrm{work} = 0$ and unable to allocate work space.

**Computational Errors:** None.

**Input-Argument Errors:**

+   1. $m < 0$  
+   2. $n < 0$  
+   3. $\mathrm{lda} \leq 0$  
+   4. $\mathrm{lda} < m$  
+   5. $l\mathrm{work} \neq 0, l\mathrm{work} \neq -1$, and $l\mathrm{work} < \mathrm{max}(1, n)$

# ## Example 1

This example shows the $\boldsymbol{Q}\boldsymbol{R}$ factorization of a general matrix $\boldsymbol{A}$ of size $6 \times 2$.

**Note:** Because $l\mathrm{work} = 0$, DGEQRF dynamically allocates the work area used by this subroutine.

**Call Statements and Input:**

```
        M     N     A     LDA   TAU     WORK    LWORK   INFO
        |     |     |     |     |       |       |       |
CALL DGEQRF ( 6 , 2 , A , 6 , TAU , WORK , 0 , INFO)
```

General matrix $\boldsymbol{A}$ of size $6 \times 2$:

$\boldsymbol{A} = \left[ \begin{array}{rr} .000000 & 2.000000 \\ 2.000000 & -1.000000 \\ 2.000000 & -1.000000 \\ .000000 & 1.500000 \\ 2.000000 & -1.000000 \\ 2.000000 & -1.000000 \end{array} \right]$

**Output:**

General matrix $\boldsymbol{A}$ of size $6 \times 2$:

$\boldsymbol{A} = \left[ \begin{array}{rr} -4.500000 & 2.000000 \\ .500000 & 2.500000 \\ .500000 & -.285714 \\ .000000 & -.428571 \\ .500000 & -.285714 \\ .500000 & .285714 \end{array} \right]$

Vector $\boldsymbol{r}$ of length 2: