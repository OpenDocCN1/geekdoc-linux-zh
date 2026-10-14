
对任意 $i$（$1\le i\le n$），可以验证

$$
1-\xi+\xi\left(\frac{\lambda_i}{w_l^T(k)Cw_l(k)}\right)\ge (1-\xi)>0,
$$

对于 $k\ge1$ 成立，其中 $0<\xi<1$。因此，必存在常数 $\tilde K_l$ 使得

$$
\left[\frac{z_j^{(l)}(k+1)}{z_l^{(l)}(k+1)}\right]^2\le \left[\frac{\xi\lambda_j+(1-\xi)\lambda_lH_l^2}{\xi\lambda_l+(1-\xi)\lambda_lH_l^2}\right]^2\left[\frac{z_j^{(l)}(k)}{z_l^{(l)}(k)}\right]^2
$$

$$
\le \left[\frac{\xi\lambda_{l+1}+(1-\xi)\lambda_lH_l^2}{\xi\lambda_l+(1-\xi)\lambda_lH_l^2}\right]^2\left[\frac{z_j^{(l)}(k)}{z_l^{(l)}(k)}\right]^2
$$

$$
=\left[\frac{z_j^{(l)}(0)}{z_l^{(l)}(0)}\right]^2e^{-\theta_l(k+1)},
$$

对 $k>\tilde K_l$ 成立。

由于 $w_l(0)\in S(H_l)$，根据引理 4.6，$z_l^{(l)}(k)$ 必定最终有界；即存在常数 $b_l>0$，使得对所有 $k\ge K_l$ 有 $(z_l^{(l)}(k))^2\le b_l$。于是，

$$
\sum_{j=l+1}^{n}(z_j^{(l)}(k))^2=\sum_{j=l+1}^{n}\left[\frac{z_j^{(l)}(k)}{z_l^{(l)}(k)}\right]^2(z_l^{(l)}(k))^2\le \Pi_l e^{-\theta_l k},
$$

对 $k\ge\max\{K_l,\tilde K_l\}$ 成立，其中

$$
\Pi_l=b_l\sum_{j=l+1}^{n}\left[\frac{z_j^{(l)}(0)}{z_l^{(l)}(0)}\right]^2\ge0.
$$

证明完毕。

## 定理 4.2

*假设* $\lim_{k\to\infty}|\phi_i(k)|=0$，$(i=1,\ldots,p)$，*且* $w_l(0)\notin V_{\lambda_l}^{\perp}$。

*对任意* $H_l\ge \widetilde{H}_l$，*如果* $w_l(0)\in S(H_l)$，*则*

$$
\lim_{k\to\infty}w_l(k)=\pm v_l.
$$

其中 $1 \leq l \leq p$。

**证明：**由引理 4.7、4.8 和 4.9 可得

$$
\begin{cases}
\displaystyle\lim_{k\to+\infty}z_i^{(l)}(k)=0, & (i=1,\ldots,l-1),\\
\displaystyle\lim_{k\to+\infty}z_l^{(l)}(k)=(z_l^{(l)})^*, & \\
\displaystyle\lim_{k\to+\infty}z_i^{(l)}(k)=0, & (i=l+1,\ldots,n).
\end{cases}
$$

于是，

$$\lim_{k\to+\infty}w_l(k)=(z_l^{(l)})^*v_l. \tag{4.15}$$

由 (4.4)，在系统稳定后，可得

$$\lim_{k\to+\infty}Cw_l(k)=\lim_{k\to+\infty}\left[\sum_{i=1}^{l-1}v_i(k)v_i^T(k)Cw_l(k)+w_l^T(k)Cw_l(k)w_l(k)\right]. \tag{4.16}$$

将 (4.15) 代入 (4.16)，可得

$$\lambda_l(z_l^{(l)})^*v_l=\lambda_l\big((z_l^{(l)})^*\big)^2(z_l^{(l)})^*v_l.$$

容易看出

$$\left((z_l^{(l)})^*\right)^2=1.$$

证毕。

在前述定理中，需要条件 $w_l(0)\notin V_l^\perp$。由于任何微小扰动都可能导致 $w_l(0)\notin V_l^\perp$，因此在实际应用中该条件容易满足。

在我们的假设中，还要求对所有 $k\geq 0$ 有 $w_l(k)\notin V_0$。由于提取的主方向与非零特征值相关联，且演化轨迹始终接近主方向，因此该条件通常能够满足。下面的引理将进一步说明这一点。

## 引理 4.10

假设 $\displaystyle\lim_{k\to+\infty}\phi_i^{(l)}(k)=0$，$(i=1,\ldots,p)$。则存在常数 $\hat K_l$，使得

$$0<\sqrt{\frac{4(1-\xi)\xi\lambda_p}{\lambda_1}}\leq\lVert w_l(k+1)\rVert\leq\frac{M_l}{\lambda_p}\sqrt{\frac{\lambda_1}{4(1-\xi)\xi\lambda_p}},$$

对所有 $k\geq\max\{K_l,\hat K_l\}$ 成立，其中 $0<\xi<1$。

**证明：**可以验证

$$\left[1-\xi+\frac{\xi\lambda_i}{w_l^T(k)Cw_l(k)}\right]^2\geq\left[1-\xi+\frac{\xi\lambda_p}{w_l^T(k)Cw_l(k)}\right]^2>0,$$

对于 $k>0$ 成立。由 (4.6)、(4.12) 和 (4.13) 可得如下 $\Gamma$：

$$
\begin{aligned}
\Gamma &= w_l^T(k+1)Cw_l(k+1) \\
&=\sum_{i=1}^{p}\lambda_i\left(z_i^{(l)}(k+1)\right)^2 \\
&=\sum_{i=1}^{p}\left[(1-\xi)z_i^{(l)}(k)+\phi_i^{(l)}(k)\right]^2\lambda_i+\sum_{i=1}^{p}\left[1-\xi+\frac{\xi\lambda_i}{w_l^T(k)Cw_l(k)}\right]\left[z_i^{(l)}(k)+\phi_i^{(l)}(k)\right]^2\lambda_i \\
&=\sum_{i=1}^{p}\left\{\left[1-\xi+\frac{\xi\lambda_i}{w_l^T(k)Cw_l(k)}\right]\left[z_i^{(l)}(k)+\phi_i^{(l)}(k)\right]\right\}^2\lambda_i \\
&=\sum_{i=1}^{p}\left\{\left[1-\xi+\frac{\xi\lambda_i}{\displaystyle\sum_{j=1}^{p}\lambda_j\left(z_j^{(l)}(k)\right)^2}\right]\left[z_i^{(l)}(k)+\phi_i^{(l)}(k)\right]\right\}^2\lambda_i \\
&=\sum_{i=1}^{p}\left\{\left[1-\xi+\frac{\xi\lambda_i}{\displaystyle\sum_{j=1}^{p}\lambda_j\left(z_j^{(l)}(k)\right)^2}\right]\left(z_i^{(l)}(k)+\phi_i^{(l)}(k)\right)\right. \\
&\qquad\left.-\frac{\xi\lambda_i z_i^{(l)}(k)\displaystyle\sum_{j=1}^{p}\lambda_j\left(z_j^{(l)}(k)\right)^2}{w_l^T(k)Cw_l(k)\displaystyle\sum_{j=1}^{p}\lambda_j\left(z_j^{(l)}(k)\right)^2}\right\}\lambda_i \\
&=\sum_{i=1}^{p}\left[1-\xi+\frac{\xi\lambda_i}{\displaystyle\sum_{j=1}^{p}\lambda_j\left(z_j^{(l)}(k)\right)^2}\right]\left(\left(z_i^{(l)}(k)\right)^2\lambda_i+\Psi_i^{(l)}(k)\right),
\end{aligned}
$$

其中
