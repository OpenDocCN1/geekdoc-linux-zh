If $m$ or $n$ is equal to 0, no computation is performed. See references [15], [60], [80], and pages 134 to 151 in reference [102]. These algorithms have a tendency to generate underflows that may hurt overall performance. The system default is to mask underflow, which improves the performance of these subroutines.

# ## Error Conditions

Computational Errors:  None

Input-Argument Errors:

+   1. $ldv \le 0$
+   2. $n > ldv$
+   3. $ldub \le 0$
+   4. $n > ldub$
+   5. $ldx \le 0$
+   6. $n > ldx$
+   7. $nb \le 0$
+   8. $m < 0$
+   9. $n < 0$
+   10. $r < 0$

# ### Example 1

This example finds the linear least squares solution for the underdetermined system $AX=B$, using the singular value decomposition computed by DGESVF.

Matrix A is:

$$ \left[ \begin{array}{ccc} 1.0 & 2.0 & 2.0 \\ 2.0 & 4.0 & 5.0 \end{array} \right] $$

and matrix B is:

$$ \left[ \begin{array}{c} 1.0 \\ 4.0 \end{array} \right] $$

On output, matrix $UTB$ is overwritten.

Note: This example corresponds to Example 3 of DGESVF on page 680.

**Call Statement and Input:**

$$ \begin{array}{cccccccccc} V & LDV & UB & LDUB & NB & S & X & LDX & M & N & TAU \\ | & | & | & | & | & | & | & | & | \\ CALL & DGESV & ( & V, & 3, & UB, & 3, & 1, & S, & X, & 3, & 2, & 3, & TAU \end{array} $$

$V = \left[ \begin{array}{ccc} -0.304 & -0.894 & 0.328 \\ -0.608 & 0.447 & 0.656 \\ -0.733 & 0.000 & -0.680 \end{array} \right]$

$UB = \left[ \begin{array}{c} -4.061 \\ 0.000 \\ -0.714 \end{array} \right]$

$S = (7.342, 0.000, 0.305)$

$TAU = 0.3993D-14$

**Output:**