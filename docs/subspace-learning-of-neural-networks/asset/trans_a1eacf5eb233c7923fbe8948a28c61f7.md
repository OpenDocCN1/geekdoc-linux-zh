

根据引理 4.6，我们有

$$
\begin{aligned}
\|\phi_l(k)\|
&=\left\|\frac{\displaystyle\sum_{i=1}^{l-1}\left[\phi_i(k)v_i^T+v_i\phi_i(k)^T+\phi_i(k)\phi_i(k)^T\right]Cw_l(k)}{w_l^T(k)Cw_l(k)}\right\|\\
&\leq \zeta\frac{\lambda_1}{\lambda_p\sqrt{2\xi(1-\xi)}\sqrt{\frac{\lambda_p}{\lambda_1}}}\times
\left\|\xi\sum_{i=1}^{l-1}\left[\phi_i(k)v_i^T+v_i\phi_i(k)^T+\phi_i(k)\phi_i(k)^T\right]\right\|.
\end{aligned}
$$

对于 $k>K_l$ 成立。根据假设 A2，$\lim_{k\to\infty}\|\phi_l(k)\|=0$。显然，$\lim_{k\to\infty}\phi_l(k)=0$。

### 引理 4.7

假设 $\lim_{k\to\infty}\phi_i(k)=0$，$(i=1,\ldots,l-1)$。则有

$$
\lim_{k\to\infty}z_i^{(l)}(k)=0,\qquad (i=1,\ldots,l-1).
$$

*证明：* 由（4.12），对任意 $i\ (i=1,\ldots,l-1)$，可得

$$
\begin{aligned}
z_i^{(l)}(k+1)&=(1-\xi)z_i^{(l)}(k)+\phi_i(k),\\
&=(1-\xi)^kz_i^{(l)}(0)+\sum_{r=1}^{k}(1-\xi)^{r-1}\phi_i(k-r)
\end{aligned}
$$

对所有 $k>0$ 成立。由于 $0<\xi<1$ 且 $\lim_{k\to\infty}\phi_i(k)=0$，因此

$$
\begin{aligned}
\lim_{k\to\infty}z_i^{(l)}(k+1)
&=\lim_{k\to\infty}\left[(1-\xi)^kz_i^{(l)}(0)+\sum_{r=1}^{k}(1-\xi)^{r-1}\phi_i(k-r)\right]\\
&=0.
\end{aligned}
$$

证明完毕。

对任意 $H_l>0$，我们定义

$$
S(H_l)=\{w_l\mid \|w_l\|\leq H_l\}.
$$

### 引理 4.8

假设 $\lim_{k\to\infty}\phi_i(k)=0$，$(i=l,\ldots,p)$。对任意 $H_l\geq \widetilde{H}_l$，如果 $w_l(0)\in S(H_l)$，则必存在常数 $\delta>0$，使得

$$
\lim_{k\to\infty}z_l^{(l)}(k)=\left(z_l^{(l)}\right)^*,
$$

且 $\left|\left(z_l^{(l)}\right)^*\right|>\delta$，其中 $\left(z_l^{(l)}\right)^*$ 是一个常数。

*证明：* 由（4.13），若 $i=l$，则

$$
z_l^{(l)}(k+1)=\left\{1-\xi+\frac{\xi\lambda_l}{w_l^T(k)Cw_l(k)}\right\}z_l^{(l)}(k)+\phi_l(k),
$$

对所有 $k>0$ 成立。由于 $\lim_{k\to\infty}\phi_i(k)=0$，$(i=l,\ldots,p)$，存在 $\widetilde{K}_l$ 使得

$$
\begin{cases}
z_l^{(l)}(k+1)>0, & \text{if }z_l^{(l)}(\widetilde{K}_l)>0\text{ for all }k\geq\widetilde{K}_l,\\
z_l^{(l)}(k+1)<0, & \text{if }z_l^{(l)}(\widetilde{K}_l)<0\text{ for all }k\geq\widetilde{K}_l.
\end{cases}
$$

由于 $w_l(0)\in S(H_l)$，根据引理 4.6，对所有 $k\geq K_l$ 有 $w_l(k)\in S(H_l)$。如果 $z_l^{(l)}(\widetilde{K}_l)>0$，则存在常数 $N_l$ 使得

$$
\left\{\frac{\xi\lambda_l}{w_l^T(k)Cw_l(k)}\right\}z_l^{(l)}(k)+\phi_l(k)<N_l,
$$

对所有 $k\geq\max\{K_l,\widetilde{K}_l\}$ 成立。由此可得

$$
\begin{aligned}
z_l^{(l)}(k+1)&\leq (1-\xi)z_l^{(l)}(k)+N_l\\
&=(1-\xi)^kz_l^{(l)}(0)+\sum_{r=1}^{k}(1-\xi)^{r-1}N_l\\
&=(1-\xi)^kz_l^{(l)}(0)+\left(1-(1-\xi)^k\right)N_l,
\end{aligned}
$$

对所有 $k\geq K_l$ 成立。由于 $0<\xi<1$，因此

$$
\lim_{k\to\infty}\left[(1-\xi)^kz_l^{(l)}(0)+\left(1-(1-\xi)^k\right)N_l\right]=N_l.
$$

显然，必存在常数 $\left(z_l^{(l)}\right)^*$ 使得

$$
\lim_{k\to\infty}z_l^{(l)}(k)=\left(z_l^{(l)}\right)^*,
$$

其中 $\left(z_l^{(l)}\right)^*$ 是一个常数。如果 $z_l^{(l)}(\widetilde{K}_l)<0$，同理可得相同结果。接下来，我们将证明存在常数 $\delta>0$ 使得 $\left|\left(z_l^{(l)}\right)^*\right|>\delta$。

如果这不成立，则意味着 $\lim_{k\to+\infty}|z_l^{(l)}(k)|=0$。我们将证明这会导致矛盾。

由于 $\lim_{k\to+\infty}\phi_i(k)=0$（$i=l,\ldots,p$），由（4.13）可得

$$
\begin{aligned}
|z_l^{(l)}(k+1)|
&=\left|\left[(1-\xi)+\frac{\xi\lambda_l}{w_l^T(k)Cw_l(k)}\right]z_l^{(l)}(k)+\phi_l(k)\right|,\\
&=\left(1-\xi+\frac{\xi\lambda_l}{w_l^T(k)Cw_l(k)}\right)|z_l^{(l)}(k)|+\phi'_l(k),
\end{aligned}
$$

对所有 $k\ge K_l$ 成立，其中 $\lim_{k\to+\infty}\phi'_l(k)=0$。且对于 $i=l+1,\ldots,n$，我们有

$$
\begin{aligned}
|z_i^{(l)}(k+1)|
&=\left|\left[(1-\xi)+\frac{\xi\lambda_i}{w_l^T(k)Cw_l(k)}\right]z_i^{(l)}(k)+\phi_i(k)\right|,\\
&=\left(1-\xi+\frac{\xi\lambda_i}{w_l^T(k)Cw_l(k)}\right)|z_i^{(l)}(k)|+\phi'_i(k),
\end{aligned}
$$

对所有 $k\ge K_l$ 成立，其中 $\lim_{k\to+\infty}\phi'_i(k)=0$。显然，

$$
\left(1-\xi+\frac{\xi\lambda_l}{w_l^T(k)Cw_l(k)}\right)\ge\left(1-\xi+\frac{\xi\lambda_i}{w_l^T(k)Cw_l(k)}\right)>0,\quad (i=l+1,\ldots,n).
$$

如果 $k$ 足够大，不难证明 $|z_i^{(l)}(k+1)|\ge |z_i^{(l)}(k)|$。因此，若 $\lim_{k\to+\infty}|z_l^{(l)}(k)|=0$，则 $\lim_{k\to+\infty}|z_i^{(l)}(k)|=0$（$i=l+1,\ldots,n$）。所以，

$$
\lim_{k\to+\infty}\sum_{i=l}^{p}\lambda_i\bigl(z_i^{(l)}(k)\bigr)^2=0.
$$

然而，由（4.7），我们有

$$
w_l(k)^TCw_l(k)=\sum_{i=1}^{l}\lambda_i\bigl(z_i^{(l)}(k)\bigr)^2+\sum_{i=l+1}^{p}\lambda_i\bigl(z_i^{(l)}(k)\bigr)^2,
$$

对所有 $k\ge 0$ 成立。根据引理 4.6 和 4.7，有

$$
\lim_{k\to+\infty}\sum_{i=1}^{p}\lambda_i\bigl(z_i^{(l)}(k)\bigr)^2>2\lambda_p\xi(1-\xi)\sqrt{\frac{\overline{\Lambda}}{\underline{\Lambda}}}>0,
$$

这与事实矛盾。这表明必存在常数 $\delta>0$ 使得 $|z_l^{(l)}|>\delta$。

证明完毕。

### 引理 4.9

假设 $\lim_{k\to\infty}|\phi_i(k)|=0$，$(i=l,\ldots,p)$，且 $w_l(0)\notin V_{\lambda_l}^{\perp}$。对任意 $H_l\ge \widetilde{H}_l$，如果 $w_l(0)\in S(H_l)$，则存在常数 $\theta_l>0$、$\Pi_l\ge0$ 和 $\widetilde{K}_l>0$，使得

$$
\sum_{j=l+1}^{n}\left(z_j^{(l)}(k)\right)^2\le \Pi_l\cdot e^{-\theta_l k},
$$

对所有 $k>\max\{K_l,\widetilde K_l\}$ 成立，其中

$$
\theta_l=\ln\left(\frac{\xi\lambda_l+(1-\xi)\lambda_lH_l^2}{\xi\lambda_{l+1}+(1-\xi)\lambda_lH_l^2}\right)^2>0.
$$

*证明：* 由于 $w_l(0)\notin V_{\lambda_l}^{\perp}$，因此 $z_l^{(l)}(0)\ne0$。于是，由（4.13），对每个 $j$（$l+1\le j\le n$），可得

$$
\left[\frac{z_j^{(l)}(k+1)}{z_l^{(l)}(k+1)}\right]^2=\left[\frac{\left(1-\xi+\dfrac{\xi\lambda_j}{w_l^T(k)Cw_l(k)}\right)z_j^{(l)}(k)+\phi_{lj}}{\left(1-\xi+\dfrac{\xi\lambda_l}{w_l^T(k)Cw_l(k)}\right)z_l^{(l)}(k)+\phi_{ll}}\right]^2
$$

$$
=\left[\frac{1-\xi+\dfrac{\xi\lambda_j}{w_l^T(k)Cw_l(k)}}{1-\xi+\dfrac{\xi\lambda_l}{w_l^T(k)Cw_l(k)}}\right]^2\cdot\left[\frac{z_j^{(l)}(k)}{z_l^{(l)}(k)}\right]^2+\psi_l(k).
$$

对所有 $k>0$ 成立，其中

$$
\begin{aligned}
\psi_l(k)={}&\left[2\left(1-\xi+\frac{\xi\lambda_l}{w_l^T(k)Cw_l(k)}\right)\right]\left(1-\xi+\frac{\xi\lambda_j}{w_l^T(k)Cw_l(k)}\right)z_j^{(l)}(k)z_l^{(l)}(k)\\
&+\left(1-\xi+\frac{\xi\lambda_l}{w_l^T(k)Cw_l(k)}\right)z_l^{(l)}(k)\phi_{lj}\\
&+\left(1-\xi+\frac{\xi\lambda_j}{w_l^T(k)Cw_l(k)}\right)z_j^{(l)}(k)\phi_{ll}\\
&+\left(1-\xi+\frac{\xi\lambda_j}{w_l^T(k)Cw_l(k)}\right)\phi_{lj}\phi_{ll}
\end{aligned}
\left[\frac{P_l(k)}{Q_l(k)^2}\right].
$$

同时，

$$
P_l(k)=\left[\left(1-\xi+\frac{\xi\lambda_j}{w_l^T(k)Cw_l(k)}\right)z_j^{(l)}(k)\right]\phi_{lj}-\left[\left(1-\xi+\frac{\xi\lambda_l}{w_l^T(k)Cw_l(k)}\right)z_l^{(l)}(k)\right]\phi_{ll}.
$$

且

$$
Q_l(k)=\left\{\left[\left(1-\xi+\frac{\xi\lambda_l}{w_l^T(k)Cw_l(k)}\right)z_l^{(l)}(k)\right]^2+\left[\left(1-\xi-\frac{\xi\lambda_l}{w_l^T(k)Cw_l(k)}\right)z_l^{(l)}(k)\right]^2\right\},
$$

对所有 $k>0$ 成立。由于 $\lim_{k\to\infty}|\phi_i(k)|=0$（$i=1,\ldots,p$），根据引理 4.6，可得 $\lim_{k\to\infty}|\psi(k)|=0$。根据引理 4.8，可得 $\lim_{k\to\infty}[Q_l(k)]^2>\delta^2$。因此容易看出 $\lim_{k\to\infty}|\psi_l(k)|=0$。

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

### 定理 4.2

*假设* $\lim_{k\to\infty}|\phi_i(k)|=0$，$(i=1,\ldots,p)$，*且* $w_l(0)\notin V_{\lambda_l}^{\perp}$。
*对任意* $H_l\ge \widetilde{H}_l$，*如果* $w_l(0)\in S(H_l)$，*则*

$$
\lim_{k\to\infty}w_l(k)=\pm v_l.
$$

