*Proof:* To complete the proof, two cases will be considered.

**Case 1:** $2 \leq \|w(k)\|^2 \leq 1 + \dfrac{2}{1-4\eta\lambda_n}$. By $\eta\lambda_1 < 0.25$, it holds from (5.7) that

$$\begin{aligned}
&1.5 + (\eta\lambda_i - 0.5)w^T(k)w(k) + \eta w^T(k)Cw(k) - 2\eta\lambda_i \\
=&\; 1 + (0.25-\eta\lambda_i)\cdot[2-w^T(k)w(k)] - 0.25w^T(k)w(k) + \eta w^T(k)Cw(k) \\
\leq&\; 1 - 0.25w^T(k)w(k) + \eta\lambda_1w^T(k)w(k) \\
<&\; 1,\quad (i=1,\ldots,n).
\end{aligned}$$

$(5.8)$

Using Lemma 5.1, it follows from (5.6) and (5.8) that

$$\begin{aligned}
\|w(k+1)\|^2
&=\sum_{i=1}^{n} z_i^2(k+1) \\
&=\sum_{i=1}^{n}\left[1.5+(\eta\lambda_i-0.5)w^T(k)w(k)+\eta w^T(k)Cw(k)-2\eta\lambda_i\right]^2\cdot z_i^2(k) \\
&\leq \|w(k)\|^2 \\
&\leq 1+\frac{2}{1-4\eta\lambda_n}.
\end{aligned}$$

$(5.9)$

**Case 2:** $\|w(k)\|^2 < 2$. By $\eta\lambda_1 < 0.25$ and Lemma 1, it follows from (5.6) and (5.7) that

$$\begin{aligned}
\|w(k+1)\|^2
&=\sum_{i=1}^{n} z_i^2(k+1) \\
&=\sum_{i=1}^{n}\left[1.5+(\eta\lambda_i-0.5)w^T(k)w(k)+\eta w^T(k)Cw(k)-2\eta\lambda_i\right]^2\cdot z_i^2(k) \\
&=\sum_{i=1}^{n}\left\{1+(0.25-\eta\lambda_i)\cdot[2-w^T(k)w(k)]\\
&\hspace{3em}-0.25w^T(k)w(k)+\eta w^T(k)Cw(k)\right\}^2\cdot z_i^2(k) \\
&\leq \left[1+(0.25-\eta\lambda_n)(2-\|w(k)\|^2)-(0.25-\eta\lambda_1)\|w(k)\|^2\right]^2\cdot\|w(k)\|^2 \\
&\leq \left[1+(0.25-\eta\lambda_n)(2-\|w(k)\|^2)\right]^2\cdot\|w(k)\|^2 \\
&\leq \max_{0\leq s\leq 1+\frac{2}{1-4\eta\lambda_n}}\left[1+(0.25-\eta\lambda_n)(2-s)\right]^2\cdot s.
\end{aligned}$$

$(5.10)$