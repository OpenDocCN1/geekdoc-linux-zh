for $k>0$. From (4.6) and (4.8), it follows that

$$\begin{aligned}
w_1^T(k+1)Cw_1(k+1)
&=\sum_{i=1}^{p}\lambda_i\left(z_i^{(1)}(k+1)\right)^2\\
&=\sum_{i=1}^{p}\left[1-\xi+\frac{\xi\lambda_i}{w_1^T(k)Cw_1(k)}\right]^2\lambda_i\left(z_i^{(1)}(k)\right)^2\\
&\geq\left[1-\xi+\frac{\xi\lambda_p}{w_1^T(k)Cw_1(k)}\right]^2\cdot w_1^T(k)Cw_1(k)\\
&\geq\min_{s>0}\left\{\left[1-\xi+\frac{\xi\lambda_p}{s}\right]^2\cdot s\right\}.
\end{aligned}$$

for $k>0$. Using Lemma 4.1, it follows that

$$w_1^T(k+1)Cw_1(k+1)>4(1-\xi)\xi\lambda_p,$$

for $k>0$. Since $\lambda_1\|w_1(k)\|^2\geq w_1^T(k)Cw_1(k)$ for $k\geq 0$, it follows that

$$\|w_1(k+1)\|\geq\sqrt{\frac{4(1-\xi)\xi\lambda_p}{\lambda_1}}>0,$$

for $k>0$. This completes the proof.  
Next, we prove that $\|w_1(k)\|$ is upper bounded.

# **Lemma 4.3**  Suppose that $w_1(0)\notin V_1^\perp$. There must exist a constant $\tilde H_1$ so that

$$\|w_1(k+1)\|<\tilde H_1,$$

for all $k>0$.

**Proof:** From (4.7), it follows that

$$\|w_1(k+1)\|\leq(1-\xi)\|w_1(k)\|+\xi\frac{\|C\|\|w_1(k)\|}{w_1^T(k)Cw_1(k)}.$$

Let $d_1=\xi\frac{\|C\|}{\lambda_p}$. It follows that

$$\begin{aligned}
\|w_1(k+1)\|&\leq(1-\xi)\|w_1(k)\|+\xi\frac{\|C\|\|w_1(k)\|}{\lambda_p\|w_1(k)\|^2}\\
&=(1-\xi)\|w_1(k)\|+\frac{d_1}{\|w_1(k)\|}\\
&=(1-\xi)^k\|w_1(0)\|+d_1\sum_{r=1}^{k}\frac{(1-\xi)^{r-1}}{\|w_1(k-r)\|}.
\end{aligned}$$