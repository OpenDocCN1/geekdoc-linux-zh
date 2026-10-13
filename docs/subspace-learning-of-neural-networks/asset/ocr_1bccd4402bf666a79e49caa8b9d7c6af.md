Let $\phi_{li}(k)=v_i^T\phi_l(k)$. Substitute (4.5) and (4.6) into (4.11), for all $k>0$, it follows that

$$z_i^{(l)}(k+1)=(1-\xi)z_i^{(l)}(k)+\phi_{li}(k), \tag{4.12}$$

for $i=1,\ldots,l-1$, and

$$z_i^{(l)}(k+1)=\left\{1-\xi+\frac{\xi\lambda_i}{w_i^T(k)Cw_i(k)}\right\}z_i^{(l)}(k)+\phi_{li}(k), \tag{4.13}$$

for $i=l,\ldots,n$, where $\phi_{li}(k)=v_i^T\phi_l(k)$.

Let

$$\widetilde{C}_l(k)=C-\sum_{i=1}^{l-1}w_i(k)w_i^T(k)C,\qquad (1\leq l\leq p),$$

for all $k>0$. According to the assumption A1, there must exist a constant $M_l$ so that $0\leq\|\widetilde{C}_l(k)\|<M_l$ for all $k\geq0$. Denote by $V_0^{(l)}(k)$, the null subspace associated with the eigenvalue $0$ of the matrix $\widetilde{C}_l(k)$ and $\Lambda_{\min}^{(l)}(k)$ the smallest nonzero eigenvalue of $\widetilde{C}_l(k).$ Clearly, $\Lambda_{\min}^{(l)}(k)>0$ for all $k>0$. From (4.4), it follows that

$$w_l(k+1)=(1-\xi)w_l(k)+\xi\frac{\widetilde{C}_l(k)w_l(k)}{w_l(k)^TCw_l(k)}, \tag{4.14}$$

for $k>0$ and $0<\xi<1$.

**Lemma 4.6** Suppose that $w_l(k)\notin V_0^{(l)}(k)$ for all $k>0$. $\|w_l(k+1)\|$ is ultimately bounded; that is, constants $K_l>0$ must exist so that

$$\sqrt{2\xi(1-\xi)\sqrt{\frac{\widetilde{\Lambda}}{\widetilde{\Lambda}_1}}}<\|w_l(k+1)\|<\widetilde{H}_l,$$

for all $k\geq K_l$, where $\widetilde{\Lambda}=\min\{\Lambda_{\min}^{(l)}(k),k\geq0\}$ and $\widetilde{H}_l=\dfrac{M_l}{\lambda_p\sqrt{2\xi(1-\xi)\sqrt{\widetilde{\Lambda}/\widetilde{\Lambda}_1}}}$.

*Proof:* From (4.14), it follows that

$$\begin{aligned}\|w_l(k+1)\|^2={}&w_l(k+1)^Tw_l(k+1)\\={}&(1-\xi)^2\|w_l(k)\|^2\\&+2\xi(1-\xi)\frac{w_l(k)^T\widetilde{C}_l(k)w_l(k)}{w_l(k)^TCw_l(k)}\\&+\xi^2\frac{w_l(k)^T\widetilde{C}_l(k)^T\widetilde{C}_l(k)w_l(k)}{[w_l(k)^TCw_l(k)]^2},\end{aligned}$$

for $k>0$. Since $w_l(k)\notin V_0^{(l)}(k)$ for all $k\geq0$ and the assumption A2, there must exist a constant $K_l$ such that

$$w_l(k)^T\widetilde{C}_l(k)w_l(k)\geq0,$$