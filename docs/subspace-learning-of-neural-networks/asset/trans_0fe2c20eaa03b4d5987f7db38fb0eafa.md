

### 引理 2.4

假设

$$\eta\sigma\leq\frac{3\sqrt{2}-2}{2}\approx 0.8899,$$

且 $w(0)\in S$, $w(0)\notin V_\sigma$。则存在常数 $\theta_2>0$ 和 $\Pi_2>0$，使得

$$\left|\sigma-w^T(k+1)Cw(k+1)\right|
\leq k\cdot\Pi_2\cdot\left[e^{-\theta_2(k+1)}+\max\left\{e^{-\theta_2k},e^{-\theta_1k}\right\}\right]$$

对所有 $k\geq 0$ 成立，其中

$$\left\{\begin{aligned}
\theta_2&=-\ln\delta,\\
\delta&=\max\left\{(1-\gamma)^2,\eta\sigma\right\},\\
\gamma&=\min\left\{(\eta\lambda_p)^3,\eta w^T(0)Cw(0)\right\},
\end{aligned}\right.$$

且 $0<\delta<1$, $0<\gamma<1$。

**证明：** 显然，

$$\begin{aligned}
w^T(k+1)Cw(k+1)
&=\sum_{i=1}^{n}\lambda_i\left[1+\eta\left(\lambda_i-w^T(k)Cw(k)\right)\right]^2z_i^2(k)\\
&=\sum_{i=1}^{n}\lambda_i\left[1+\eta\left(\sigma-w^T(k)Cw(k)\right)\right]^2z_i^2(k)\\
&\quad+\sum_{i=m+1}^{n}\lambda_i\left[1+\eta\left(\lambda_i-w^T(k)Cw(k)\right)\right]^2z_i^2(k)\\
&\quad-\sum_{i=m+1}^{n}\lambda_i\left[1+\eta\left(\sigma-w^T(k)Cw(k)\right)\right]^2z_i^2(k)\\
&=\left[1+\eta\left(\sigma-w^T(k)Cw(k)\right)\right]^2w^T(k)Cw(k)+H(k),
\end{aligned}$$

对于 $k\ge 0$，其中

$$H(k)=\eta\sum_{i=m+1}^{n}\lambda_i(\lambda_i-\sigma)\times\left[2+\eta\left(\lambda_i+\sigma-2w^T(k)Cw(k)\right)\right]z_i^2(k).$$

于是，

$$\begin{aligned}
\sigma-w^T(k+1)Cw(k+1)
&=\left[\sigma-w^T(k)Cw(k)\right]\\
&\quad\times\left[\left(1-\eta w^T(k)Cw(k)\right)^2-\eta^2\sigma w^T(k)Cw(k)\right]\\
&\quad-H(k),
\end{aligned}$$

对于 $k\ge 0$。记

$$V(k)=\left|\sigma-w^T(k)Cw(k)\right|,$$

对于 $k\ge 0$。由 $S$ 的不变性，对 $k\ge 0$ 有 $w(k)\in S$。由此可得

$$\begin{aligned}
V(k+1)
&\le V(k)\cdot\left|\left(1-\eta w^T(k)Cw(k)\right)^2-\eta^2\sigma w^T(k)Cw(k)\right|+|H(k)|\\
&\le \max\left\{\left(1-\eta w^T(k)Cw(k)\right)^2,\eta^2\sigma w^T(k)Cw(k)\right\}\cdot V(k)+|H(k)|\\
&\le \max\left\{\left(1-\eta w^T(k)Cw(k)\right)^2,\eta\sigma\right\}\cdot V(k)+|H(k)|.
\end{aligned}$$

记

$$\gamma=\min\left\{(\eta\lambda_p)^3,\eta w^T(0)Cw(0)\right\}.$$

显然，$0<\gamma<1$。由引理 2.3 可知

$$\gamma \leq \eta\,w^T(k)Cw(k) \leq 1.$$

记

$$\delta=\max\left\{(1-\gamma)^2,\,\eta\sigma\right\}.$$

显然，$0<\delta<1$。则

$$V(k+1)\leq\delta\cdot V(k)+|H(k)|,\ k\geq 0.$$

由引理 2.2，

$$\begin{aligned}
|H(k)|
&\leq \eta\sum_{j=m+1}^{n}\lambda_j(\sigma-\lambda_j)\left[\eta(\sigma+\lambda_j)+2\right]z_j^2(k)\\
&\leq \eta\sum_{j=m+1}^{n}\left[\eta\lambda_j(\sigma^2-\lambda_j^2)+2\lambda_j(\sigma-\lambda_j)\right]z_j^2(k)\\
&\leq \eta\sum_{j=m+1}^{n}\left(\eta\lambda_j\sigma^2+2\lambda_j\sigma\right)z_j^2(k)\\
&\leq \sigma(\eta\sigma+2)\sum_{j=m+1}^{n}z_j^2(k)\\
&\leq 3\sigma\cdot\sum_{j=m+1}^{n}z_j^2(k)\\
&\leq 3\sigma\Pi_1\cdot e^{-\theta_1 k}.
\end{aligned}$$

对所有 $k\geq 0$ 成立。则

$$\begin{aligned}
V(k+1)
&\leq \delta^{k+1}V(0)+3\sigma\Pi_1\cdot\sum_{r=0}^{k}\delta^{k-r}e^{-\theta_1 r}\\
&\leq \delta^{k+1}V(0)+3k\sigma\Pi_1\max\{\delta^k,e^{-\theta_1 k}\}\\
&\leq k\cdot\Pi_2\cdot\left[e^{-\theta_2(k+1)}+\max\{e^{-\theta_2 k},e^{-\theta_1 k}\}\right],
\end{aligned}$$

其中 $\theta_2=-\ln\delta>0$ 且

$$\Pi_2=\max\left\{\left|\sigma-w^T(0)Cw(0)\right|,\,3\sigma\Pi_1\right\}>0.$$

证明完毕。

### 引理 2.5

假设存在常数 $\theta>0$ 和 $\Pi>0$，使得

$$\eta\left|\left(\sigma-w^T(k)Cw(k)\right)z_i(k)\right|\leq k\cdot\Pi e^{-\theta k},\quad (i=1,\ldots,m)$$

对于 $k \ge 0$ 成立。则

$$\lim_{k\to+\infty} z_i(k)=z_i^*,\quad (i=1,\ldots,m),$$

其中 $z_i^* (i=1,\ldots,m)$ 为常数。

**证明：** 对任意 $\epsilon>0$，存在 $K\ge 1$，使得

$$\frac{\Pi K e^{-\theta K}}{(1-e^{-\theta})^2}\le \epsilon.$$

对任意 $k_1>k_2\ge K$，有

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

这表明每个序列 $\{z_i(k)\}$ 都是**柯西序列**。根据*柯西收敛原理*，必存在常数 $z_i^*$ $(i=1,\ldots,m)$，使得

$$\lim_{k\to+\infty}z_i(k)=z_i^*,\quad (i=1,\ldots,m).$$

证明完毕。

### 定理 2.3

假设

$$\eta\sigma\le\frac{3\sqrt{3}-2}{2}\approx0.8899,$$

若 $w(0)\in S$ 且 $w(0)\notin V_\sigma^\perp$，则 (2.2) 从 $w(0)$ 出发的轨迹将收敛到与协方差矩阵 $C$ 的最大特征值相关联的唯一特征向量。

**证明：** 由引理 2.2，存在常数 $\theta_1>0$ 和 $\Pi_1\geq 0$，使得

$$\sum_{j=m+1}^{n} z_j^2(k)\leq \Pi_1e^{-\theta_1k},$$

对所有 $k\geq 0$ 成立。由引理 2.4，存在常数 $\theta_2>0$ 和 $\Pi_2>0$，使得

$$\left|\sigma-w^T(k+1)Cw(k+1)\right|\leq k\cdot\Pi_2\cdot\left[e^{-\theta_2(k+1)}+\max\left\{e^{-\theta_2k},e^{-\theta_1k}\right\}\right]$$

对所有 $k\geq 0$ 成立。

显然，存在常数 $\theta>0$ 和 $\Pi>0$，使得

$$\eta\left|(\sigma-w^T(k)Cw(k))\,z_i(k)\right|\leq k\cdot\Pi e^{-\theta k},\quad (i=1,\ldots,m)$$

对于 $k\geq 0$ 成立。

利用引理 2.5 和引理 2.2，可得

$$\left\{\begin{aligned}\lim_{k\to+\infty}z_i(k)&=z_i^*,\quad(i=1,\ldots,m),\\\lim_{k\to+\infty}z_i(k)&=0,\quad(i=m+1,\ldots,n).\end{aligned}\right.$$

则

$$\lim_{k\to+\infty}w(k)=\sum_{i=1}^{m}z_i^*v_i\in V_\sigma.$$

容易看出

$$\sum_{i=1}^{m}(z_i^*)^2=1.$$

证明完毕。

在上述定理中，要求初始值 $w(0)\notin V_\sigma^\perp$，从而至少存在一个 $z_i(0)\neq 0\ (1\leq i\leq m)$。由于 $V_\sigma^\perp$ 的维数小于 $R^n$ 的维数，$V_\sigma^\perp$ 的测度为零，因此条件 $w(0)\notin V_\sigma^\perp$ 在实际应用中很容易满足。事实上，任何微小的扰动都会导致 $w(0)\notin V_\sigma^\perp$。从这个角度来看，我们可以推断，几乎所有从 $S$ 出发的轨迹都将收敛到与协方差矩阵 $C$ 的最大特征值对应的单位特征向量。此外，值得指出的是，$w(0)\notin V_\sigma^\perp$ 蕴含 $w(0)\neq 0$。

## 2.3.4 仿真与讨论

### 2.3.4.1 不变集的图示

定理 2.1 给出了一个不变集 $S$，而定理 2.2 给出了一族不变集 $S(l)\ (1\leq l\leq 2)$。显然，$S\subset S(l)$。我们首先说明 $S(2)$（定理 2.2 中最大的不变集）的不变性。考虑 (2.2) 的一个简单二维例子，其中

$$C=\begin{bmatrix}1 & 0\\0 & 0.2\end{bmatrix}.$$

容易看出

$$S(2)=\left\{\begin{bmatrix}w_1\\w_2\end{bmatrix}\ \middle|\ w_1^2+0.2w_2^2\le 1.6481\right\}.$$

在图 2.1 中，椭圆所包含的部分即为 $S(2)$。图 2.1 显示，当 $\eta=1.3811$ 时，从 $S(2)$ 中的点出发的 (2.2) 的 80 条轨迹经过 5000 次迭代后仍全部包含在 $S(2)$ 中。这清楚地表明了 $S(2)$ 的不变性。

![](img/5d1bf22d32ba379cbf31221a5347fdb6_50_0.png)

**图 2.1**  
$S(2)$ 的不变性。从 $S(2)$ 中的点出发的 80 条轨迹仍保持在 $S(2)$ 中。

虽然集合 $S(2)$ 是不变的，但这并不意味着 $S(2)$ 中的每条轨迹都收敛。事实上，$S(2)$ 中包含的某些轨迹可能不收敛。图 2.2 显示了从 $w(0)=[0.2,2.5]^T$ 出发、$\eta=1.3811$ 时的这样一条不收敛轨迹。

### 2.3.4.2 初始向量的选取

定理 2.3 表明，从 $S-\{0\}$ 出发的轨迹将收敛到与最大特征值对应的单位特征向量。因此，从 $S$ 中选择初始向量对收敛至关重要。然而，这种选择需要矩阵 $C$ 的信息。一般来说，这并不实际。接下来，我们提出一个更实际的初始向量选取区域。

