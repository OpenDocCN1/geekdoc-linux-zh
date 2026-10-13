
By Lemma 4.6, we have

$$
\begin{aligned}
\|\phi_l(k)\|
&=\left\|\frac{\displaystyle\sum_{i=1}^{l-1}\left[\phi_i(k)v_i^T+v_i\phi_i(k)^T+\phi_i(k)\phi_i(k)^T\right]Cw_l(k)}{w_l^T(k)Cw_l(k)}\right\|\\
&\leq \zeta\frac{\lambda_1}{\lambda_p\sqrt{2\xi(1-\xi)}\sqrt{\frac{\lambda_p}{\lambda_1}}}\times
\left\|\xi\sum_{i=1}^{l-1}\left[\phi_i(k)v_i^T+v_i\phi_i(k)^T+\phi_i(k)\phi_i(k)^T\right]\right\|.
\end{aligned}
$$

for $k>K_l$. By assumption A2, $\lim_{k\to\infty}\|\phi_l(k)\|=0$. Clearly, $\lim_{k\to\infty}\phi_l(k)=0$.

### Lemma 4.7

Suppose that $\lim_{k\to\infty}\phi_i(k)=0$, $(i=1,\ldots,l-1)$. It holds that

$$
\lim_{k\to\infty}z_i^{(l)}(k)=0,\qquad (i=1,\ldots,l-1).
$$

*Proof:* From (4.12), given any $i\ (i=1,\ldots,l-1)$, it follows that

$$
\begin{aligned}
z_i^{(l)}(k+1)&=(1-\xi)z_i^{(l)}(k)+\phi_i(k),\\
&=(1-\xi)^kz_i^{(l)}(0)+\sum_{r=1}^{k}(1-\xi)^{r-1}\phi_i(k-r)
\end{aligned}
$$

for all $k>0$. Since $0<\xi<1$ and $\lim_{k\to\infty}\phi_i(k)=0$, it holds that

$$
\begin{aligned}
\lim_{k\to\infty}z_i^{(l)}(k+1)
&=\lim_{k\to\infty}\left[(1-\xi)^kz_i^{(l)}(0)+\sum_{r=1}^{k}(1-\xi)^{r-1}\phi_i(k-r)\right]\\
&=0.
\end{aligned}
$$

The proof is completed.

Given any $H_l>0$, we define

$$
S(H_l)=\{w_l\mid \|w_l\|\leq H_l\}.
$$

### Lemma 4.8

Suppose that $\lim_{k\to\infty}\phi_i(k)=0$, $(i=l,\ldots,p)$. Given any $H_l\geq \widetilde{H}_l$, if $w_l(0)\in S(H_l)$, there must exist a constant $\delta>0$ so that

$$
\lim_{k\to\infty}z_l^{(l)}(k)=\left(z_l^{(l)}\right)^*,
$$

and $\left|\left(z_l^{(l)}\right)^*\right|>\delta$, where $\left(z_l^{(l)}\right)^*$ is a constant.

*Proof:* From (4.13), if $i=l$, it follows that

$$
z_l^{(l)}(k+1)=\left\{1-\xi+\frac{\xi\lambda_l}{w_l^T(k)Cw_l(k)}\right\}z_l^{(l)}(k)+\phi_l(k),
$$

for all $k>0$. Since $\lim_{k\to\infty}\phi_i(k)=0$, $(i=l,\ldots,p)$, there exists a $\widetilde{K}_l$ so that

$$
\begin{cases}
z_l^{(l)}(k+1)>0, & \text{if }z_l^{(l)}(\widetilde{K}_l)>0\text{ for all }k\geq\widetilde{K}_l,\\
z_l^{(l)}(k+1)<0, & \text{if }z_l^{(l)}(\widetilde{K}_l)<0\text{ for all }k\geq\widetilde{K}_l.
\end{cases}
$$

Since $w_l(0)\in S(H_l)$, by Lemma 4.6, $w_l(k)\in S(H_l)$ for all $k\geq K_l$. If $z_l^{(l)}(\widetilde{K}_l)>0$, there exists a constant $N_l$ so that

$$
\left\{\frac{\xi\lambda_l}{w_l^T(k)Cw_l(k)}\right\}z_l^{(l)}(k)+\phi_l(k)<N_l,
$$

for all $k\geq\max\{K_l,\widetilde{K}_l\}$. It follows that

$$
\begin{aligned}
z_l^{(l)}(k+1)&\leq (1-\xi)z_l^{(l)}(k)+N_l\\
&=(1-\xi)^kz_l^{(l)}(0)+\sum_{r=1}^{k}(1-\xi)^{r-1}N_l\\
&=(1-\xi)^kz_l^{(l)}(0)+\left(1-(1-\xi)^k\right)N_l,
\end{aligned}
$$

for all $k\geq K_l$. Since $0<\xi<1$, it holds that

$$
\lim_{k\to\infty}\left[(1-\xi)^kz_l^{(l)}(0)+\left(1-(1-\xi)^k\right)N_l\right]=N_l.
$$

Clearly, there must exist a constant $\left(z_l^{(l)}\right)^*$ so that

$$
\lim_{k\to\infty}z_l^{(l)}(k)=\left(z_l^{(l)}\right)^*,
$$

where $\left(z_l^{(l)}\right)^*$ is a constant. If $z_l^{(l)}(\widetilde{K}_l)<0$, the same result can be obtained similarly. Next, we will prove that there exists a constant $\delta>0$ so that $\left|\left(z_l^{(l)}\right)^*\right|>\delta$.

If this is not true, then it means $\lim_{k\to+\infty}|z_l^{(l)}(k)|=0$. We will prove that it leads to a contradiction.

Since $\lim_{k\to+\infty}\phi_i(k)=0$ ($i=l,\ldots,p$), from (4.13), it follows that

$$
\begin{aligned}
|z_l^{(l)}(k+1)|
&=\left|\left[(1-\xi)+\frac{\xi\lambda_l}{w_l^T(k)Cw_l(k)}\right]z_l^{(l)}(k)+\phi_l(k)\right|,\\
&=\left(1-\xi+\frac{\xi\lambda_l}{w_l^T(k)Cw_l(k)}\right)|z_l^{(l)}(k)|+\phi'_l(k),
\end{aligned}
$$

for all $k\ge K_l$, where $\lim_{k\to+\infty}\phi'_l(k)=0$. And for $i=l+1,\ldots,n$, we have

$$
\begin{aligned}
|z_i^{(l)}(k+1)|
&=\left|\left[(1-\xi)+\frac{\xi\lambda_i}{w_l^T(k)Cw_l(k)}\right]z_i^{(l)}(k)+\phi_i(k)\right|,\\
&=\left(1-\xi+\frac{\xi\lambda_i}{w_l^T(k)Cw_l(k)}\right)|z_i^{(l)}(k)|+\phi'_i(k),
\end{aligned}
$$

for all $k\ge K_l$, where $\lim_{k\to+\infty}\phi'_i(k)=0$. Clearly,

$$
\left(1-\xi+\frac{\xi\lambda_l}{w_l^T(k)Cw_l(k)}\right)\ge\left(1-\xi+\frac{\xi\lambda_i}{w_l^T(k)Cw_l(k)}\right)>0,\quad (i=l+1,\ldots,n).
$$

If $k$ is sufficiently large, it is not difficult to show that $|z_i^{(l)}(k+1)|\ge |z_i^{(l)}(k)|$. Thus, if $\lim_{k\to+\infty}|z_l^{(l)}(k)|=0$, then $\lim_{k\to+\infty}|z_i^{(l)}(k)|=0$ ($i=l+1,\ldots,n$). So,

$$
\lim_{k\to+\infty}\sum_{i=l}^{p}\lambda_i\bigl(z_i^{(l)}(k)\bigr)^2=0.
$$

However, from (4.7), we have

$$
w_l(k)^TCw_l(k)=\sum_{i=1}^{l}\lambda_i\bigl(z_i^{(l)}(k)\bigr)^2+\sum_{i=l+1}^{p}\lambda_i\bigl(z_i^{(l)}(k)\bigr)^2,
$$

for all $k\ge 0$. From Lemmas 4.6 and 4.7, it holds that

$$
\lim_{k\to+\infty}\sum_{i=1}^{p}\lambda_i\bigl(z_i^{(l)}(k)\bigr)^2>2\lambda_p\xi(1-\xi)\sqrt{\frac{\overline{\Lambda}}{\underline{\Lambda}}}>0,
$$

which is a contradiction. This shows that there must exist a constant $\delta>0$ so that $|z_l^{(l)}|>\delta$.

This completes the proof.

### Lemma 4.9

Suppose that $\lim_{k\to\infty}|\phi_i(k)|=0$, $(i=l,\ldots,p)$, and $w_l(0)\notin V_{\lambda_l}^{\perp}$. Given any $H_l\ge \widetilde{H}_l$, if $w_l(0)\in S(H_l)$, then there exist constants $\theta_l>0$, $\Pi_l\ge0$, and $\widetilde{K}_l>0$ such that

$$
\sum_{j=l+1}^{n}\left(z_j^{(l)}(k)\right)^2\le \Pi_l\cdot e^{-\theta_l k},
$$

for all $k>\max\{K_l,\widetilde K_l\}$, where

$$
\theta_l=\ln\left(\frac{\xi\lambda_l+(1-\xi)\lambda_lH_l^2}{\xi\lambda_{l+1}+(1-\xi)\lambda_lH_l^2}\right)^2>0.
$$

*Proof:* Since $w_l(0)\notin V_{\lambda_l}^{\perp}$, then $z_l^{(l)}(0)\ne0$. Then, from (4.13), for each $j$ $(l+1\le j\le n)$, it follows that

$$
\left[\frac{z_j^{(l)}(k+1)}{z_l^{(l)}(k+1)}\right]^2=\left[\frac{\left(1-\xi+\dfrac{\xi\lambda_j}{w_l^T(k)Cw_l(k)}\right)z_j^{(l)}(k)+\phi_{lj}}{\left(1-\xi+\dfrac{\xi\lambda_l}{w_l^T(k)Cw_l(k)}\right)z_l^{(l)}(k)+\phi_{ll}}\right]^2
$$

$$
=\left[\frac{1-\xi+\dfrac{\xi\lambda_j}{w_l^T(k)Cw_l(k)}}{1-\xi+\dfrac{\xi\lambda_l}{w_l^T(k)Cw_l(k)}}\right]^2\cdot\left[\frac{z_j^{(l)}(k)}{z_l^{(l)}(k)}\right]^2+\psi_l(k).
$$

for all $k>0$, where

$$
\begin{aligned}
\psi_l(k)={}&\left[2\left(1-\xi+\frac{\xi\lambda_l}{w_l^T(k)Cw_l(k)}\right)\right]\left(1-\xi+\frac{\xi\lambda_j}{w_l^T(k)Cw_l(k)}\right)z_j^{(l)}(k)z_l^{(l)}(k)\\
&+\left(1-\xi+\frac{\xi\lambda_l}{w_l^T(k)Cw_l(k)}\right)z_l^{(l)}(k)\phi_{lj}\\
&+\left(1-\xi+\frac{\xi\lambda_j}{w_l^T(k)Cw_l(k)}\right)z_j^{(l)}(k)\phi_{ll}\\
&+\left(1-\xi+\frac{\xi\lambda_j}{w_l^T(k)Cw_l(k)}\right)\phi_{lj}\phi_{ll}
\end{aligned}
\left[\frac{P_l(k)}{Q_l(k)^2}\right].
$$

Meanwhile,

$$
P_l(k)=\left[\left(1-\xi+\frac{\xi\lambda_j}{w_l^T(k)Cw_l(k)}\right)z_j^{(l)}(k)\right]\phi_{lj}-\left[\left(1-\xi+\frac{\xi\lambda_l}{w_l^T(k)Cw_l(k)}\right)z_l^{(l)}(k)\right]\phi_{ll}.
$$

and

$$
Q_l(k)=\left\{\left[\left(1-\xi+\frac{\xi\lambda_l}{w_l^T(k)Cw_l(k)}\right)z_l^{(l)}(k)\right]^2+\left[\left(1-\xi-\frac{\xi\lambda_l}{w_l^T(k)Cw_l(k)}\right)z_l^{(l)}(k)\right]^2\right\},
$$

for all $k>0$. Since $\lim_{k\to\infty}|\phi_i(k)|=0$ $(i=1,\ldots,p)$, by Lemma 4.6, it follows that $\lim_{k\to\infty}|\psi(k)|=0$. By Lemma 4.8, it follows that $\lim_{k\to\infty}[Q_l(k)]^2>\delta^2$. So, it is easy to see that $\lim_{k\to\infty}|\psi_l(k)|=0$.

Given any $i(1\le i\le n)$, it can be checked that

$$
1-\xi+\xi\left(\frac{\lambda_i}{w_l^T(k)Cw_l(k)}\right)\ge (1-\xi)>0,
$$

for $k\ge1$, where $0<\xi<1$. Thus, there must exist a constant $\tilde K_l$ so that

$$
\left[\frac{z_j^{(l)}(k+1)}{z_l^{(l)}(k+1)}\right]^2\le \left[\frac{\xi\lambda_j+(1-\xi)\lambda_lH_l^2}{\xi\lambda_l+(1-\xi)\lambda_lH_l^2}\right]^2\left[\frac{z_j^{(l)}(k)}{z_l^{(l)}(k)}\right]^2
$$

$$
\le \left[\frac{\xi\lambda_{l+1}+(1-\xi)\lambda_lH_l^2}{\xi\lambda_l+(1-\xi)\lambda_lH_l^2}\right]^2\left[\frac{z_j^{(l)}(k)}{z_l^{(l)}(k)}\right]^2
$$

$$
=\left[\frac{z_j^{(l)}(0)}{z_l^{(l)}(0)}\right]^2e^{-\theta_l(k+1)},
$$

for $k>\tilde K_l$.

Since $w_l(0)\in S(H_l)$, by Lemma 4.6, $z_l^{(l)}(k)$ must be ultimately bounded; that is, there exists a constant $b_l>0$ such that $(z_l^{(l)}(k))^2\le b_l$ for all $k\ge K_l$. Then,

$$
\sum_{j=l+1}^{n}(z_j^{(l)}(k))^2=\sum_{j=l+1}^{n}\left[\frac{z_j^{(l)}(k)}{z_l^{(l)}(k)}\right]^2(z_l^{(l)}(k))^2\le \Pi_l e^{-\theta_l k},
$$

for $k\ge\max\{K_l,\tilde K_l\}$, where

$$
\Pi_l=b_l\sum_{j=l+1}^{n}\left[\frac{z_j^{(l)}(0)}{z_l^{(l)}(0)}\right]^2\ge0.
$$

This completes the proof.

### Theorem 4.2

*Suppose that* $\lim_{k\to\infty}|\phi_i(k)|=0$, $(i=1,\ldots,p)$ *and* $w_l(0)\notin V_{\lambda_l}^{\perp}$.
*Given any* $H_l\ge \widetilde{H}_l$, *if* $w_l(0)\in S(H_l)$, *then*

$$
\lim_{k\to\infty}w_l(k)=\pm v_l.
$$
