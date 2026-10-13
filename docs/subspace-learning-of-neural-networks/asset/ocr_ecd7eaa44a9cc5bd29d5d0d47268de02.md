# ### 3.4　Convergence Analysis of Oja’s Algorithms with Adaptive Learning Rate

In this section, details associated with a convergence analysis of the proposed learning algorithm will be provided systematically.

# #### 3.4.1　Boundedness

First, we will analyze the boundedness of the system (3.5). The lower and upper bounds of the system evolution will be given in following theorems.

**Lemma 3.2** Suppose that $0<\xi<0.8$, if $0<w^T(k)Cw(k)<\lambda_p$, then $w^T(k)Cw(k)$ is increasing.

*Proof:* If $w^T(k)Cw(k)\leq\lambda_p$, it can be checked that

$$\left[1+\xi\left(\frac{\lambda_i}{w^T(k)Cw(k)}-1\right)\right]^2\geq\left[1+\xi\left(\frac{\lambda_p}{w^T(k)Cw(k)}-1\right)\right]^2\geq1,$$

for $k\geq0$. Then, from (3.5), (1.7), and (3.6), we have

$$\begin{aligned} w^T(k+1)Cw(k+1)&=\sum_{i=1}^{p}\left[1+\xi\left(\frac{\lambda_i}{w^T(k)Cw(k)}-1\right)\right]^2\lambda_i z_i^2(k)\\ &\geq\left[1+\xi\left(\frac{\lambda_p}{w^T(k)Cw(k)}-1\right)\right]^2w^T(k)Cw(k)\\ &\geq w^T(k)Cw(k). \end{aligned}$$

for $k\geq0$. The proof is complete.

**Theorem 3.1** If $w(0)\notin\mathcal{V}_{\sigma}^{\perp}$, it holds that

$$w^T(k+1)Cw(k+1)\geq4(1-\xi)\xi\lambda_p>0,$$

for all $k\geq0$, where $0<\xi<0.8$.

*Proof:* It can be checked that

$$\left[1+\xi\left(\frac{\lambda_i}{w^T(k)Cw(k)}-1\right)\right]^2\geq\left[1+\xi\left(\frac{\lambda_p}{w^T(k)Cw(k)}-1\right)\right]^2>0.$$