using the standard formulas for $\sum_{k=1}^{n} k^{2}$ and $\sum_{k=1}^{n} k$, adapted to the case where the sums begin with $k=2$. It follows, after doing the algebra, that $r_{n}=\frac{2}{3} n^{3}-\frac{1}{2} n^{2}+\frac{5}{6} n-1$. This agrees with the solution to Problem 7.8 that we have already given.

# 7.7.1.A  a. Suppose that $\beta_{1}, \beta_{2}, \ldots, \beta_{k}$ are constants such that

$\beta_{1}\{r_{1}^{n}\}+\beta_{2}\{r_{2}^{n}\}+\ldots+\beta_{k}\{r_{k}^{n}\}=\{0\}.$ (1)

It follows that all the terms of the sequence on the left-hand side of Equation 1 are equal to $0$. In particular, we have that

$\beta_{1} r_{1}+\beta_{2} r_{2}+\ldots+\beta_{k} r_{k}=0 \n\beta_{1} r_{1}^{2}+\beta_{2} r_{2}^{2}+\ldots+\beta_{k} r_{k}^{2}=0 \n\vdots \n\beta_{1} r_{1}^{k}+\beta_{2} r_{2}^{k}+\ldots+\beta_{k} r_{k}^{k}=0$

It follows that

$\mathbf{A}_{k} \mathbf{v}_{k}=\mathbf{0}$, (2)

where

$\mathbf{A}_{k}=\begin{pmatrix} r_{1} & r_{2} & \cdots & r_{k} \ r_{1}^{2} & r_{2}^{2} & \cdots & r_{k}^{2} \ \vdots & \vdots & \cdots & \vdots \ r_{1}^{k} & r_{2}^{k} & \cdots & r_{k}^{k} \end{pmatrix}$ and $\mathbf{v}_{k}=\begin{pmatrix} \beta_{1} \ \beta_{2} \ \vdots \ \beta_{k} \end{pmatrix}$.

It is straightforward to show (or a standard algebraic fact that you already know) that $\det(\mathbf{A}_{k})=r_{1} r_{2} \ldots r_{k} \prod_{1 \leq i<j \leq k}\left(r_{j}-r_{i}\right)$, and, hence, if the numbers $r_{1}, r_{2}, \ldots, r_{k}$ are all different, $\det(\mathbf{A}_{k}) \neq 0$. It follows that the matrix $\mathbf{A}_{k}$ is invertible. Hence by Equation 2, $\mathbf{v}_{k}=\mathbf{A}_{k}^{-1} \mathbf{0}=\mathbf{0}$. Therefore $\beta_{1}=\beta_{2}=\ldots=\beta_{k}=0$. It follows that the vectors $\{r_{1}^{n}\},\{r_{2}^{n}\}, \ldots,\{r_{k}^{n}\}$ are linearly independent.

ii. Let $\left\{z_{n}\right\}$ be a solution of the recurrence relation $\alpha_{q} a_{n}+\alpha_{q} a_{n-1}+\ldots+\alpha_{k} a_{n-k}=0$. Since the sequences $\{y(1), y(2),\ldots,\}(y(k))_{n}$ are solutions of this recurrence relation, so too is the sequence $\left\{\mathbf{w}_{n}\right\}$, where, for each positive integer $n, w_{n}=z_{1} y(1)_{n}+z_{2} y(2)_{n}+\ldots+z_{k} y(k)_{n}$. Then, for $1 \leq i \leq k, w_{i}=z_{1} y(1)_{i}+z_{2} y(2)_{i}+\ldots+z_{k} y(k)_{i}=z_{i}$. Since subsequent terms of the sequences $\left\{w_{n}\right\}$ and $\left\{z_{n}\right\}$ are given by the same recurrence relation, the sequences $\left\{w_{n}\right\}$ and $\left\{z_{n}\right\}$ are identical. Therefore $\left\{z_{n}\right\}$ is