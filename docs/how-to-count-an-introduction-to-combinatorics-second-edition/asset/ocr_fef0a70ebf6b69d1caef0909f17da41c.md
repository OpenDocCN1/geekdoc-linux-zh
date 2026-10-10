+   ii.  For $1 \leq i \leq k$, let $\{y(i)_n\}$ be the solution of the above recurrence relation
+   that satisfies the initial conditions

$y(i)_n = \begin{cases} 1, & \text{if } n = i, \ 0, & \text{otherwise}. \end{cases}$

Prove that the set of sequences $\{y(1)_n\}, \{y(2)_n\}, \ldots, \{y(k)_n\}$ forms a spanning set for the solution space, $S$, of the recurrence relation in Equation 7.7.2.

+   iii.  Prove that, if $x_1, x_2, \ldots, x_k$ are $k$ distinct solutions of the polynomial equation

$\alpha_kx^k + \alpha_{k-1}x^{k-1} + \ldots + \alpha_1x + \alpha_0 = 0,$

then every solution of the above recurrence relation has the form

$\{A_1x_1^n + A_2x_2^n + \ldots + A_kx_k^n\}$

for some appropriate choice of the constants $A_1, A_2, \ldots, A_k$.

# **7.7.1B**  *Repeated roots of the auxiliary equation*

Prove that if $x_a$ is a nonzero solution of the polynomial equation $b_dx^{n+k} + b_{n+1}x^{n-1} + \ldots + b_{n-1}x + b_n = 0$ of multiplicity $r$, then the sequences $\{x_a^n\}$, $\{nx_a^n\}$, $\ldots$, $\{n^{r-1}x_a^n\}$ form a set of $r$ linearly independent solutions of the recurrence relation $b_na_n + b_{n+1}a_{n-1} + \ldots + b_{n+k}a_{n-k} = 0$.

# **7.7.2A**  Find the solution of the following recurrence relations.

+   i.  $a_n - 10a_{n-1} + 25a_{n-2} = 0$, subject to the initial conditions $a_1 = 15$ and $a_2 = 325$.

+   ii.  $a_n + 4a_{n-1} + 4a_{n-2} = 0$, subject to the initial conditions $a_1 = 4$ and $a_2 = 4$.

+   iii.  $a_n - 7a_{n-1} + 16a_{n-2} - 12a_{n-3} = 0$, subject to the initial conditions $a_1 = 8$, $a_2 = 42$, and $a_3 = 142$.

+   iv.  $a_n - 6a_{n-1} + 12a_{n-2} - 8a_{n-3} = 0$, subject to the initial conditions $a_1 = 0$, $a_2 = 8$, and $a_3 = 16$.

# **7.7.2B**  Find the solution of the following recurrence relations.

+   i.  $a_n + 10a_{n-1} + 25a_{n-2} = 0$, subject to the initial conditions $a_1 = 15$ and $a_2 = 325$.

+   ii.  $a_n - 4a_{n-1} + 4a_{n-2} = 0$, subject to the initial conditions $a_1 = 0$ and $a_2 = 4$.

+   iii.  $a_n - 9a_{n-1} + 27a_{n-2} - 27a_{n-3} = 0$, subject to the initial conditions $a_1 = 0$, $a_2 = 0$, and $a_3 = 54$.

+   iv.  $a_n - 4a_{n-1} - 3a_{n-2} + 18a_{n-3} = 0$, subject to the initial conditions $a_1 = 4$, $a_2 = -29$, and $a_3 = 40$.

# **7.8** SOME NONLINEAR RECURRENCE RELATIONS

When it comes to nonlinear recurrence relations, life becomes much more difficult. In this section we consider nonlinear recurrence relations of just one type. This type has been chosen because it occurs naturally in some counting problems and, by good fortune, also succumbs to the generating function method.