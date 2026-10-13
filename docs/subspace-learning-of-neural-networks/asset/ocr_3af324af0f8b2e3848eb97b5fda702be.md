# **Lemma 4.9** Suppose that \(\lim_{k\to\infty}|\phi_i|=0\), \((i=l,\ldots,p)\), and \(w_l(0)\notin V_{\lambda_l}^{\perp}\). Given any \(H_l\ge H_i\), if \(w_l(0)\in S(H_l)\), then there exist constant \(\theta_l>0\), \(\Pi_l\ge0\), and \(\widetilde K_l>0\) such that

\[\sum_{j=l+1}^{n}\left(z_j^{(l)}(k)\right)^2\le \Pi_l\cdot e^{-\theta_l k},\]

for all \(k>\max\{K_l,\widetilde K_l\}\), where

\[\theta_l=\ln\left(\frac{\xi\lambda_l+(1-\xi)\lambda_lH_l^2}{\xi\lambda_{l+1}+(1-\xi)\lambda_{l+1}H_l^2}\right)^2>0.\]

**Proof:** Since \(w_l(0)\notin V_{\lambda_l}^{\perp}\), then \(z_j^{(l)}(0)\ne0\). Then, from (4.13), for each \(j\) \((l+1\le j\le n)\), it follows that

\[\left[\frac{z_j^{(l)}(k+1)}{z_l^{(l)}(k+1)}\right]^2=\left[\frac{\left(1-\xi+\dfrac{\xi\lambda_j}{w_l^T(k)Cw_l(k)}\right)z_j^{(l)}(k)+\phi_{lj}}{\left(1-\xi+\dfrac{\xi\lambda_l}{w_l^T(k)Cw_l(k)}\right)z_l^{(l)}(k)+\phi_{ll}}\right]^2\]

\[=\left[\frac{1-\xi+\dfrac{\xi\lambda_j}{w_l^T(k)Cw_l(k)}}{1-\xi+\dfrac{\xi\lambda_l}{w_l^T(k)Cw_l(k)}}\right]^2\cdot\left[\frac{z_j^{(l)}(k)}{z_l^{(l)}(k)}\right]^2+\psi_l(k).\]

for all \(k>0\), where

\[\begin{aligned}\psi_l(k)={}&\left[2\left(1-\xi+\frac{\xi\lambda_l}{w_l^T(k)Cw_l(k)}\right)\right]\left(1-\xi+\frac{\xi\lambda_j}{w_l^T(k)Cw_l(k)}\right)z_j^{(l)}(k)z_l^{(l)}(k)\\&+\left(1-\xi+\frac{\xi\lambda_l}{w_l^T(k)Cw_l(k)}\right)z_l^{(l)}(k)\phi_{lj}\\&+\left(1-\xi+\frac{\xi\lambda_j}{w_l^T(k)Cw_l(k)}\right)z_j^{(l)}(k)\phi_{ll}\\&+\left(1-\xi+\frac{\xi\lambda_j}{w_l^T(k)Cw_l(k)}\right)\phi_{lj}\phi_{ll}\end{aligned}\left[\frac{P_l(k)}{Q_l(k)^2}\right].\]

Meanwhile,

\[P_l(k)=\left[\left(1-\xi+\frac{\xi\lambda_j}{w_l^T(k)Cw_l(k)}\right)z_j^{(l)}(k)\right]\phi_{lj}-\left[\left(1-\xi+\frac{\xi\lambda_l}{w_l^T(k)Cw_l(k)}\right)z_l^{(l)}(k)\right]\phi_{ll}.\]