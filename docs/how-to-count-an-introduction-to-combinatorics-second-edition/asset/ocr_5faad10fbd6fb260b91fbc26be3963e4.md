α,β are the roots of the quadratic equation $x^2-2x-1 = 0$, from which it follows that $α, β$ are $1 ± \sqrt{2}$. Thus, the general solution of the recurrence relation is $a_n = A(1 + \sqrt{2})^n + B(1 - \sqrt{2})^n$. Since $a_1 = 3$, we have

$(1+\sqrt{2})A+(1-\sqrt{2})B=3.$

Since $a_2 = 7$ and $(1±\sqrt{2})^2 = 1 ± 2\sqrt{2} + 2 = 3 ± 2\sqrt{2}$,

$(3+2\sqrt{2})A+(3-2\sqrt{2})B=7.$

Solving Equations 1 and 2 gives $A = \frac{1}{2}(1+\sqrt{2})$ and $B = \frac{1}{2}(1 - \sqrt{2})$. Hence $a_n = \frac{1}{2}((1+\sqrt{2})^{n+1} +(1-\sqrt{2})^{n+1}).$

# **7.5.3A**

By expanding the determinant down the first column, we see that

$\text{det}(A_n) = \begin{vmatrix} 1&1&0&0&\cdots&0&0&0 \\ 1&1&1&0&\cdots&0&0&0 \\ 0&1&1&1&\cdots&0&0&0 \\ \vdots&\vdots&\vdots&\vdots&&\vdots&\vdots&\vdots \\ \vdots&\vdots&\vdots&\vdots&&\vdots&\vdots&\vdots \\ 0&0&0&0&\cdots&1&1&0 \\ 0&0&0&0&\cdots&1&1&1 \\ 0&0&0&0&\cdots&0&1&1 \end{vmatrix} - \begin{vmatrix} 1&0&0&0&\cdots&0&0&0 \\ 1&1&1&0&\cdots&0&0&0 \\ 0&1&1&1&\cdots&0&0&0 \\ \vdots&\vdots&\vdots&\vdots&&\vdots&\vdots&\vdots \\ \vdots&\vdots&\vdots&\vdots&&\vdots&\vdots&\vdots \\ 0&0&0&0&\cdots&1&1&0 \\ 0&0&0&0&\cdots&1&1&1 \\ 0&0&0&0&\cdots&0&1&1 \end{vmatrix}$

$= \text{det}(A_{n-1}) - \begin{vmatrix} 1&1&0&\cdots&0&0&0 \\ 1&1&1&\cdots&0&0&0 \\ \vdots&\vdots&\vdots&&\vdots&\vdots&\vdots \\ \vdots&\vdots&\vdots&&\vdots&\vdots&\vdots \\ 0&0&0&\cdots&1&1&0 \\ 0&0&0&\cdots&1&1&1 \\ 0&0&0&\cdots&0&1&1 \end{vmatrix} = \text{det}(A_{n-1}) - \text{det}(A_{n-2}),$

on expanding the second determinant in Equation 1 along the top row. Hence, the required recurrence relation is

$d_n = d_{n-1} - d_{n-2}$, with $a_1 = ||d_1 = 1$ and $a_2 = \begin{bmatrix} 1&1 \\ 1&1 \end{bmatrix} = 0.$

The auxiliary equation associated with Equation 2 is $x^2 - x + 1 = 0$. This has the complex roots $α, β = \frac{1}{2}(1 ± \sqrt{-3}i)$. Hence the general solution is $a_n = A(\frac{1}{2}(1 + \sqrt{3}i))^n + B(\frac{1}{2}(1 - \sqrt{3}i))^n$ for