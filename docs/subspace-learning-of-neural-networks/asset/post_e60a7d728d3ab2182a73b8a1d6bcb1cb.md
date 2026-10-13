
### Lemma 2.4

Suppose that

$$\eta\sigma\leq\frac{3\sqrt{2}-2}{2}\approx 0.8899,$$

and $w(0)\in S$, $w(0)\notin V_\sigma$. Then, there exists constants $\theta_2>0$ and $\Pi_2>0$ such that

$$\left|\sigma-w^T(k+1)Cw(k+1)\right|
\leq k\cdot\Pi_2\cdot\left[e^{-\theta_2(k+1)}+\max\left\{e^{-\theta_2k},e^{-\theta_1k}\right\}\right]$$

for all $k\geq 0$, where

$$\left\{\begin{aligned}
\theta_2&=-\ln\delta,\\
\delta&=\max\left\{(1-\gamma)^2,\eta\sigma\right\},\\
\gamma&=\min\left\{(\eta\lambda_p)^3,\eta w^T(0)Cw(0)\right\},
\end{aligned}\right.$$

and $0<\delta<1$, $0<\gamma<1$.

**Proof:** Clearly,

$$\begin{aligned}
w^T(k+1)Cw(k+1)
&=\sum_{i=1}^{n}\lambda_i\left[1+\eta\left(\lambda_i-w^T(k)Cw(k)\right)\right]^2z_i^2(k)\\
&=\sum_{i=1}^{n}\lambda_i\left[1+\eta\left(\sigma-w^T(k)Cw(k)\right)\right]^2z_i^2(k)\\
&\quad+\sum_{i=m+1}^{n}\lambda_i\left[1+\eta\left(\lambda_i-w^T(k)Cw(k)\right)\right]^2z_i^2(k)\\
&\quad-\sum_{i=m+1}^{n}\lambda_i\left[1+\eta\left(\sigma-w^T(k)Cw(k)\right)\right]^2z_i^2(k)\\
&=\left[1+\eta\left(\sigma-w^T(k)Cw(k)\right)\right]^2w^T(k)Cw(k)+H(k),
\end{aligned}$$

for $k\ge 0$, where

$$H(k)=\eta\sum_{i=m+1}^{n}\lambda_i(\lambda_i-\sigma)\times\left[2+\eta\left(\lambda_i+\sigma-2w^T(k)Cw(k)\right)\right]z_i^2(k).$$

Then,

$$\begin{aligned}
\sigma-w^T(k+1)Cw(k+1)
&=\left[\sigma-w^T(k)Cw(k)\right]\\
&\quad\times\left[\left(1-\eta w^T(k)Cw(k)\right)^2-\eta^2\sigma w^T(k)Cw(k)\right]\\
&\quad-H(k),
\end{aligned}$$

for $k\ge 0$. Denote

$$V(k)=\left|\sigma-w^T(k)Cw(k)\right|,$$

for $k\ge 0$. By the invariance of $S$, $w(k)\in S$ for $k\ge 0$. It follows that

$$\begin{aligned}
V(k+1)
&\le V(k)\cdot\left|\left(1-\eta w^T(k)Cw(k)\right)^2-\eta^2\sigma w^T(k)Cw(k)\right|+|H(k)|\\
&\le \max\left\{\left(1-\eta w^T(k)Cw(k)\right)^2,\eta^2\sigma w^T(k)Cw(k)\right\}\cdot V(k)+|H(k)|\\
&\le \max\left\{\left(1-\eta w^T(k)Cw(k)\right)^2,\eta\sigma\right\}\cdot V(k)+|H(k)|.
\end{aligned}$$

Denote

$$\gamma=\min\left\{(\eta\lambda_p)^3,\eta w^T(0)Cw(0)\right\}.$$

Clearly, $0<\gamma<1$. By Lemma 2.3, it holds that

$$\gamma \leq \eta\,w^T(k)Cw(k) \leq 1.$$

Denote

$$\delta=\max\left\{(1-\gamma)^2,\,\eta\sigma\right\}.$$

Clearly, $0<\delta<1$. Then,

$$V(k+1)\leq\delta\cdot V(k)+|H(k)|,\ k\geq 0.$$

By Lemma 2.2,

$$\begin{aligned}
|H(k)|
&\leq \eta\sum_{j=m+1}^{n}\lambda_j(\sigma-\lambda_j)\left[\eta(\sigma+\lambda_j)+2\right]z_j^2(k)\\
&\leq \eta\sum_{j=m+1}^{n}\left[\eta\lambda_j(\sigma^2-\lambda_j^2)+2\lambda_j(\sigma-\lambda_j)\right]z_j^2(k)\\
&\leq \eta\sum_{j=m+1}^{n}\left(\eta\lambda_j\sigma^2+2\lambda_j\sigma\right)z_j^2(k)\\
&\leq \sigma(\eta\sigma+2)\sum_{j=m+1}^{n}z_j^2(k)\\
&\leq 3\sigma\cdot\sum_{j=m+1}^{n}z_j^2(k)\\
&\leq 3\sigma\Pi_1\cdot e^{-\theta_1 k}.
\end{aligned}$$

for all $k\geq 0$. Then,

$$\begin{aligned}
V(k+1)
&\leq \delta^{k+1}V(0)+3\sigma\Pi_1\cdot\sum_{r=0}^{k}\delta^{k-r}e^{-\theta_1 r}\\
&\leq \delta^{k+1}V(0)+3k\sigma\Pi_1\max\{\delta^k,e^{-\theta_1 k}\}\\
&\leq k\cdot\Pi_2\cdot\left[e^{-\theta_2(k+1)}+\max\{e^{-\theta_2 k},e^{-\theta_1 k}\}\right],
\end{aligned}$$

where $\theta_2=-\ln\delta>0$ and

$$\Pi_2=\max\left\{\left|\sigma-w^T(0)Cw(0)\right|,\,3\sigma\Pi_1\right\}>0.$$

The proof is completed.

### Lemma 2.5

Suppose there exists constants $\theta>0$ and $\Pi>0$ such that

$$\eta\left|\left(\sigma-w^T(k)Cw(k)\right)z_i(k)\right|\leq k\cdot\Pi e^{-\theta k},\quad (i=1,\ldots,m)$$

for $k \ge 0$. Then,

$$\lim_{k\to+\infty} z_i(k)=z_i^*,\quad (i=1,\ldots,m),$$

where $z_i^* (i=1,\ldots,m)$ are constants.

**Proof:** Given any $\epsilon>0$, there exists a $K\ge 1$ such that

$$\frac{\Pi K e^{-\theta K}}{(1-e^{-\theta})^2}\le \epsilon.$$

For any $k_1>k_2\ge K$, it follows that

$$\begin{aligned}
|z_i(k_1)-z_i(k_2)|
&=\left|\sum_{r=k_2}^{k_1-1}[z_i(r+1)-z_i(r)]\right|\\
&\le \eta\sum_{r=k_2}^{k_1-1}|(\sigma-w^T(r)Cw(r))z_i(r)|\\
&\le \Pi\sum_{r=k_2}^{k_1-1}e^{-\theta r}\\
&\le \Pi\sum_{r=K}^{+\infty}e^{-\theta r}\\
&\le \Pi K e^{-\theta K}\sum_{r=0}^{+\infty}(e^{-\theta})^{r-1}\\
&=\frac{\Pi K e^{-\theta K}}{(1-e^{-\theta})^2}\\
&\le \epsilon,\quad (i=1,\ldots,m).
\end{aligned}$$

This shows that each sequence $\{z_i(k)\}$ is a **Cauchy sequence**. By *Cauchy Convergence Principle*, there must exist constants $z_i^*$ $(i=1,\ldots,m)$ such that

$$\lim_{k\to+\infty}z_i(k)=z_i^*,\quad (i=1,\ldots,m).$$

This completes the proof.

### Theorem 2.3

Suppose that

$$\eta\sigma\le\frac{3\sqrt{3}-2}{2}\approx0.8899,$$

if $w(0)\in S$ and $w(0)\notin V_\sigma^\perp$, then the trajectory of (2.2) starting from $w(0)$ will converge to a unique eigenvector associated with the largest eigenvalue of the covariance matrix $C$.

**Proof:** By Lemma 2.2, there exists constants $\theta_1>0$ and $\Pi_1\geq 0$ such that

$$\sum_{j=m+1}^{n} z_j^2(k)\leq \Pi_1e^{-\theta_1k},$$

for all $k\geq 0$. By Lemma 2.4, there exists constants $\theta_2>0$ and $\Pi_2>0$ such that

$$\left|\sigma-w^T(k+1)Cw(k+1)\right|\leq k\cdot\Pi_2\cdot\left[e^{-\theta_2(k+1)}+\max\left\{e^{-\theta_2k},e^{-\theta_1k}\right\}\right]$$

for all $k\geq 0$.

Obviously, there exists constants $\theta>0$ and $\Pi>0$ such that

$$\eta\left|(\sigma-w^T(k)Cw(k))\,z_i(k)\right|\leq k\cdot\Pi e^{-\theta k},\quad (i=1,\ldots,m)$$

for $k\geq 0$.

Using Lemma 2.5 and Lemma 2.2, it follows that

$$\left\{\begin{aligned}\lim_{k\to+\infty}z_i(k)&=z_i^*,\quad(i=1,\ldots,m),\\\lim_{k\to+\infty}z_i(k)&=0,\quad(i=m+1,\ldots,n).\end{aligned}\right.$$

Then,

$$\lim_{k\to+\infty}w(k)=\sum_{i=1}^{m}z_i^*v_i\in V_\sigma.$$

It is easy to see that

$$\sum_{i=1}^{m}(z_i^*)^2=1.$$

The proof is completed.

In the above theorem, it requires that the initial $w(0)\notin V_\sigma^\perp$ so that there is at least one $z_i(0)\neq 0\ (1\leq i\leq m)$. Since the dimension of $V_\sigma^\perp$ is less than that of $R^n$, the measure of $V_\sigma^\perp$ is zero, the condition $w(0)\notin V_\sigma^\perp$ is easy to meet in practical applications. In fact, any small disturbance can result in $w(0)\notin V_\sigma^\perp$. From this perspective, we can deduce that almost all trajectories starting from $S$ will converge to a unit eigenvector associated with the largest eigenvalue of the covariance matrix of $C$. Also, it is worthwhile to point out that $w(0)\notin V_\sigma^\perp$ implies $w(0)\neq 0$.

## 2.3.4 Simulation and Discussions

### 2.3.4.1 Illustration of Invariant Sets

Theorem 2.1 gives an invariant set $S$, while Theorem 2.2 gives a family of invariant sets $S(l)\ (1\leq l\leq 2)$. Clearly, $S\subset S(l)$. Let us first illustrate the invariance of $S(2)$, the largest invariant set in Theorem 2.2. Consider a simple example of (2.2) with two dimension, where

$$C=\begin{bmatrix}1 & 0\\0 & 0.2\end{bmatrix}.$$

It is easy to see that

$$S(2)=\left\{\begin{bmatrix}w_1\\w_2\end{bmatrix}\ \middle|\ w_1^2+0.2w_2^2\le 1.6481\right\}.$$

In Figure 2.1, the ellipsoid contained part is $S(2)$. Figure 2.1 shows that 80 trajectories of (2.2) starting from points in $S(2)$ are all contained in $S(2)$ for 5000 iterations with $\eta=1.3811$. It clearly shows the invariance of $S(2)$.

![](img/5d1bf22d32ba379cbf31221a5347fdb6_50_0.png)

**FIGURE 2.1**  
Invariance of $S(2)$. Eighty trajectories starting from points in $S(2)$ remain in $S(2)$.

Though the set $S(2)$ is invariant, it does not imply that each trajectory in $S(2)$ is convergent. In fact, some trajectories contained in $S(2)$ may not converge. Figure 2.2 shows such a nonconvergent trajectory starting from $w(0)=[0.2,2.5]^T$ with $\eta=1.3811$.

### 2.3.4.2 Selection of Initial Vectors

Theorem 2.3 shows that trajectories starting from $S-\{0\}$ will converge to a unit eigenvector associated with the largest eigenvalue. Thus, choosing initial vectors from $S$ is essential for convergence. However, this selection needs information of the matrix $C$. Generally, it is not practical. Next, a more practical domain for initial vector selection is suggested.
