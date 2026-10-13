**Theorem 6.3** Suppose that \(z(0)\in S_{z_1}\), \(z(0)\notin V_1^\perp\) and \(\Gamma_z>\max\{K\,\mathrm{Kurt}(s_{j_0})+3,3\}\). If \(\mathrm{Kurt}(s_{j_0})z_{j_0}^2(0)>\eta\,\Gamma_z\), \(j_0\in Q\) and \(i\in T/j_0\), there must exist a constant \(z_{j_0}^*\) so that \(\lim_{k\to+\infty}E\{w(k)\}=Bz(k)=b_{j_0}\cdot z_{j_0}^*\).

*Proof:* By Lemmas 6.6 and 6.8, when \(k\) is large enough, it follows that

$$z_{j_0}(k+1)=z_{j_0}(k)+[\eta a-\eta a z_{j_0}^{2}(k)+\eta b(\mathrm{Kurt}(s_{j_0})z_{j_0}^{2}(k)+3z_{j_0}^{2}(k))]z_{j_0}(k).$$

Give any \(\tau>0\), there exists a \(K\geq 1\) such that

$$|\eta a-V(0)|\sqrt{\frac{1+\eta a}{\eta a}}\frac{\zeta^K}{1-\zeta}<\tau.$$

For any \(k_1>k_2\geq K\), it follows that

$$\begin{aligned}|z_{j_0}(k_1)-z_{j_0}(k_2)|&=\left|\sum_{i=k_2}^{k_1-1}(z_{j_0}(i+1)-z_{j_0}(i))\right|\\&=\left|\sum_{i=k_2}^{k_1-1}[(\eta a-V(i))z_{j_0}(i)]\right|\\&\leq\sum_{i=k_2}^{k_1-1}|\eta a-V(i)|\,|z_{j_0}(i)|\\&\leq\sqrt{\frac{1+\eta a}{\eta a}}\sum_{i=k_2}^{k_1-1}|\eta a-V(i)|.\end{aligned}$$

By Lemma 6.9, it holds that

$$\begin{aligned}|z_{j_0}(k_1)-z_{j_0}(k_2)|&\leq\sqrt{\frac{1+\eta a}{\eta a}}\sum_{i=k_2}^{\infty}|\eta a-V(0)|\zeta^{i-1}\\&\leq|\eta a-V(0)|\sqrt{\frac{1+\eta a}{\eta a}}\frac{\zeta^{k_2-1}}{1-\zeta}\\&\leq\tau.\end{aligned}$$

This shows the sequence \(\{z_{j_0}(k)\}\) is a Cauchy sequence. By Cauchy convergence principle, there must exist a \(z_{j_0}^*\) so that \(\lim_{k\to+\infty}z_{j_0}(k)=z_{j_0}^*\). The proof is complete.

Theorem 6.3 shows the average evolution of the algorithm (6.1) converges to an independent component direction with a positive kurtosis. The analysis can be similarly used to study the convergence of (6.2). The results can be obtained as follows.

**Theorem 6.4** Suppose \(z(0)\in S_{z_2}\) and \(z(0)\notin V_1^\perp\). If \(-K\,\mathrm{Kurt}(s_{j_0})z_{j_0}^{2}(0)>-K\,\mathrm{Kurt}(s_i)z_i^{2}(0)\), \(i\in P\), and \(i\in T/i_0\), there must exist a constant \(z_{j_0}^*\) so that \(\lim_{k\to+\infty}E\{w(k)\}=b_{j_0}\cdot z_{j_0}^*\), where \(\mathrm{Kurt}(s_{i_0})<0\).