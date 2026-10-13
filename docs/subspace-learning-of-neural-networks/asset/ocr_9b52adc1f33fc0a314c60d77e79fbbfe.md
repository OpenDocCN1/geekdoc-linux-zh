# **Lemma 2.11**  Suppose there exists constants \(\theta>0\) and \(\Pi>0\) such that

\[\eta\left|\left(\sigma\left(2-\|w(k)\|^2\right)-w^T(k)Cw(k)\right)z_i(k)\right|\leq k\cdot\Pi e^{-\theta k},\quad (i=1,\ldots,m)\]\nfor \(k\geq N\). Then

\[\lim_{k\to+\infty}z_i(k)=z_i^*,\quad (i=1,\ldots,m),\]

where \(z_i^*\) \((i=1,\ldots,m)\) are constants.

*Proof:* Given any \(\epsilon>0\), there exists a \(K\geq 1\) such that

\[\frac{\Pi K e^{-\theta K}}{(1-e^{-\theta})^2}\leq\epsilon.\]

For any \(k_1>k_2\geq K\), it follows that

\[\begin{aligned}
|z_i(k_1)-z_i(k_2)|
&=\left|\sum_{r=k_2}^{k_1-1}[z_i(r+1)-z_i(r)]\right|\\
&\leq \eta\sum_{r=k_2}^{k_1-1}\left|(\sigma(2-\|w(r)\|^2)-w^T(r)Cw(r))z_i(r)\right|\\
&\leq \Pi\sum_{r=k_2}^{k_1-1}re^{-\theta r}\\
&\leq \Pi\sum_{r=K}^{+\infty}re^{-\theta r}\\
&\leq \Pi K e^{-\theta K}\cdot\sum_{r=0}^{+\infty}r(e^{-\theta})^{r-1}\\
&=\frac{\Pi K e^{-\theta K}}{(1-e^{-\theta})^2}\\
&\leq\epsilon,\quad (i=1,\ldots,m).
\end{aligned}\]

This shows that each sequence \(\{z_i(k)\}\) is a *Cauchy sequence*. By *Cauchy Convergence Principle*, there must exist constants \(z_i^*\) \((i=1,\ldots,m)\) such that

\[\lim_{k\to+\infty}z_i(k)=z_i^*,\quad (i=1,\ldots,m).\]

This completes the proof.

# **Theorem 2.6**  Suppose that

\[\eta\sigma\leq 0.25.\]

If \(w(0)\in S\) and \(w(0)\notin V_\perp\), then the trajectory of (2.12) starting from \(w(0)\) will converge to and a unit eigenvector associated with the largest eigenvalue of the covariance matrix \(C\).