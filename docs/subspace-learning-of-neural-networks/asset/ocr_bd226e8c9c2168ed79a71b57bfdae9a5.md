and

$$Q(k)=\sum_{i=m+1}^{n}\lambda_i\left[2(1-\xi)+\frac{\xi(\lambda_i+\sigma)}{w^T(k)Cw(k)}\right]\left[\frac{\xi(\sigma-\lambda_i)}{w^T(k)Cw(k)}\right]z_i^2(k),\qquad (3.11)$$

for all $k\ge 0$. Clearly, $P(k)\ge 0$ and $Q(k)\ge 0$ for all $k\ge 0$.

# **Lemma 3.4** It holds that

$$w^T(k+1)Cw(k+1)=P(k)-Q(k)$$

for $k\ge 0$.

*Proof.* From (1.8) and (3.6), it follows that

$$\begin{aligned}
w^T(k+1)Cw(k+1)
&=\sum_{i=1}^{n}\lambda_i\left[1+\xi\left(\frac{\lambda_i}{w^T(k)Cw(k)}-1\right)\right]^2z_i^2(k)\\
&=\sum_{i=1}^{n}\lambda_i\left[1+\xi\left(\frac{\sigma}{w^T(k)Cw(k)}-1\right)\right]^2z_i^2(k)\\
&=\sum_{i=m+1}^{n}\lambda_i\left[2(1-\xi)+\frac{\xi(\lambda_i+\sigma)}{w^T(k)Cw(k)}\right]\left[\frac{\xi(\sigma-\lambda_i)}{w^T(k)Cw(k)}\right]z_i^2(k)\\
&=\left[1+\xi\left(\frac{\sigma}{w^T(k)Cw(k)}-1\right)\right]^2w^T(k)Cw(k)\\
&\quad-\sum_{i=m+1}^{n}\lambda_i\left[2(1-\xi)+\frac{\xi(\lambda_i+\sigma)}{w^T(k)Cw(k)}\right]\left[\frac{\xi(\sigma-\lambda_i)}{w^T(k)Cw(k)}\right]z_i^2(k)\\
&=P(k)-Q(k).
\end{aligned}$$

The proof is complete.

# **Lemma 3.5** If $w(0)\notin V_\sigma^+$, it holds that

$$P(k-1)\ge 4(1-\xi)\xi\sigma,$$

for $k\ge 1$.

*Proof.* From (3.10), it follows that

$$\begin{aligned}
P(k-1)&=\left[1+\xi\left(\frac{\sigma}{w^T(k-1)Cw(k-1)}-1\right)\right]^2w^T(k-1)Cw(k-1)\\
&\ge \min_{s>0}\left\{\left[1+\xi\left(\frac{\sigma}{s}-1\right)\right]^2s\right\}.
\end{aligned}$$

for $k\ge 1$. By Lemma (3.1), it holds that

$$P(k-1)\ge 4(1-\xi)\xi\sigma,\qquad k\ge 1.$$

The proof is complete.