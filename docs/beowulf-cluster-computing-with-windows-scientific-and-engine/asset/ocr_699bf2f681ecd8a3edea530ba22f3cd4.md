![](bbox=[0.25, 0.15, 0.75, 0.45])

For values of $u$ along the boundary (e.g., at $x = 0$ or $y = 1$), the value of the boundary condition $g$ is used. If $h = 1/(n + 1)$ (so there are $n \times n$ points in the interior of the mesh), this gives us $n^{2}$ simultaneous linear equations to solve.

Many methods can be used to solve these equations. In fact, if you have this particular problem, you should use one of the numerical libraries described in Table 10.1. In this section, we describe a very simple (and inefficient) algorithm because, from a parallel computing perspective, it illustrates how to program more effective and general methods. The method that we use is called the *Jacobi* method for solving systems of linear equations. The Jacobi method computes successive approximations to the solution of Equation 9.3.3 by rewriting the equation as follows:

```
$\begin{aligned} u_{i+1,j} \quad & -2u_{i,j}+u_{i-1,j}+u_{i,j+1}-2u_{i,j}+u_{i,j-1} =h^{2} f(x_{i},y_{j}) \\ u_{i,j} \quad &=\frac{1}{4}\left(u_{i+1,j}+u_{i-1,j}+u_{i,j+1}+u_{i,j-1}-h^{2}f_{i,j}\right). \end{aligned}\tag{9.3.4}$
```

Each step in the Jacobi iteration computes a new approximation to $u_{i,j}^{N+1}$ in terms of the surrounding values of $u^{N}$:

```
$$ u_{i,j}^{N+1}=\frac{1}{4}\left(u_{i+1,j}^{N}+u_{i-1,j}^{N}+u_{i,j+1}^{N}+u_{i,j-1}^{N}-h^{2}f_{i,j}\right). \tag{9.3.5}$$
```