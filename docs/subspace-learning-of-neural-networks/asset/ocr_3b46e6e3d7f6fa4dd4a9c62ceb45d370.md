From Theorem 2.5, it follows that

$$V(k+1) \leq \max\left\{\left(1-\eta w^T(k)Cw(k)\right)^2,\,2\eta\sigma\right\}\cdot V(k)+|Q(k)|,$$

for $k>N$. Denote

$$\gamma=\min\left\{(2\eta\lambda_p)^2(\eta\lambda_p/\sigma),\,\eta w^T(0)Cw(0)\right\}.$$

Clearly, $0<\gamma<1$. By Lemma 2.9, it holds that

$$\gamma\leq \eta w^T(k)Cw(k)\leq 1.$$

Denote

$$\delta=\max\left\{(1-\gamma)^2,\,2\eta\sigma\right\}.$$

Clearly, $0<\delta<1$. Then

$$V(k+1)\leq\delta\cdot V(k)+|Q(k)|,\ k\geq N.$$

By Lemma 2.8,

$$\begin{aligned}
|Q(k)|&\leq \eta\sum_{j=m+1}^{n}2\lambda_j(\sigma-\lambda_j)\left[2+2\eta(\sigma+\lambda_j)z_j^2(k)\right]\\
&\leq \eta\sum_{j=m+1}^{n}4\left[\eta\lambda_j(\sigma^2-\lambda_j^2)+\lambda_j(\sigma-\lambda_j)\right]z_j^2(k)\\
&\leq \eta\sum_{j=m+1}^{n}4\left(\eta\lambda_j\sigma^2+2\lambda_j\sigma\right)z_j^2(k)\\
&\leq 4\sigma(\eta\sigma)(\eta\sigma+2)\sum_{j=m+1}^{n}z_j^2(k)\\
&\leq 12\sigma\cdot\eta\sum_{j=m+1}^{n}z_j^2(k)\\
&\leq 12\sigma\Pi_1\cdot e^{-\theta_1 k}
\end{aligned}$$

for all $k\geq N$. Then

$$\begin{aligned}
V(k+1)&\leq \delta^{k+1}V(0)+12\sigma\Pi_1\sum_{r=0}^{k}(\delta e^{\theta_1})^r e^{-\theta_1 k}\\
&\leq \delta^{k+1}V(0)+12\sigma\Pi_1\cdot\max\{\delta^k,\,e^{-\theta_1 k}\}\\
&\leq k\cdot\Pi_2\left[e^{-(\theta_2+1)k}+\max\{e^{-\theta_2 k},e^{-\theta_1 k}\}\right],
\end{aligned}$$

where $\theta_2=-\ln\delta>0$ and

$$\Pi_2=\max\left\{2\sigma-w^T(0)Cw(0),\,12\sigma\Pi_1\right\}>0.$$

The proof is completed.