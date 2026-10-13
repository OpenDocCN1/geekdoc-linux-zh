Solving

$$\ln(1+\eta\sigma) \approx \ln\left(\frac{1}{\eta\sigma}\right),$$

it follows that

$$\eta\sigma \approx 0.618.$$

This shows that one can set $\eta\sigma$ around 0.618 to achieve fast convergence. The next simulations will support this.

We randomly generated a $5 \times 5$ symmetric nonnegative definite matrix as

$$C=\begin{bmatrix}
0.1947 & 0.3349 & 0.2783 & 0.1494 & 0.0364 \\
0.3349 & 0.8052 & 0.5105 & 0.1716 & 0.0361 \\
0.2783 & 0.5105 & 0.4149 & 0.1916 & 0.0348 \\
0.1494 & 0.1716 & 0.1916 & 0.1608 & 0.0518 \\
0.0364 & 0.0361 & 0.0348 & 0.0518 & 0.0262
\end{bmatrix}.$$

Selecting an initial vector randomly in $U-\{0\}$ as

$$w(0)=\begin{bmatrix}0.0706,\ 0.2185,\ 0.0776,\ 0.3105,\ 0.4214\end{bmatrix}^{T}.$$

Figure 2.3 shows the trajectory of (2.2) starting from $w(0)$ converging to an eigenvector

$$w^{*}=\begin{bmatrix}0.3574,\ 0.7322,\ 0.5299,\ 0.2296,\ 0.0510\end{bmatrix}^{T}$$

in 17 iterations with precision $\epsilon=0.00001$ and $\eta\sigma=0.62$. Clearly, $w^{*}$ is a unit eigenvector associated with the largest eigenvalue of $C$.

![](bbox=[0.287, 0.562, 0.744, 0.821])

# FIGURE 2.3

Convergence of (2.2).

To further illustrate that by setting $\eta\sigma$ around 0.618, the DDT algorithm