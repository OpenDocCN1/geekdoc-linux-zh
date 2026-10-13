By Lemma 4.6, we have

\[
\begin{aligned}
\|\phi_l(k)\|
&=\left\|\frac{\displaystyle\sum_{i=1}^{l-1}\left[\phi_i(k)v_i^T+v_i\phi_i(k)^T+\phi_i(k)\phi_i(k)^T\right]Cw_l(k)}{w_l^T(k)Cw_l(k)}\right\|\\
&\leq \left\|\frac{\displaystyle\sum_{i=1}^{l-1}\left[\phi_i(k)v_i^T+v_i\phi_i(k)^T+\phi_i(k)\phi_i(k)^T\right]Cw_l(k)}{w_l^T(k)Cw_l(k)}\right\|\\
&\leq \zeta\frac{\lambda_1}{\lambda_p\sqrt{2\xi(1-\xi)}\sqrt{\frac{\lambda_p}{\lambda_1}}}\times
\left\|\xi\sum_{i=1}^{l-1}\left[\phi_i(k)v_i^T+v_i\phi_i(k)^T+\phi_i(k)\phi_i(k)^T\right]\right\|.
\end{aligned}
\]

for $k>K_l$. By assumption A2, $\lim_{k\to\infty}\|\phi_l(k)\|=0$. Clearly, $\lim_{k\to\infty}\phi_l(k)=0$.

# **Lemma 4.7** Suppose that $\lim_{k\to\infty}\phi_i(k)=0$, $(i=1,\ldots,l-1)$. It holds that

\[
\lim_{k\to\infty}z_i^{(l)}(k)=0,\qquad (i=1,\ldots,l-1).
\]

*Proof:* From (4.12), given any $i\ (i=1,\ldots,l-1)$, it follows that

\[
\begin{aligned}
z_i^{(l)}(k+1)&=(1-\xi)z_i^{(l)}(k)+\phi_i(k),\\
&=(1-\xi)^kz_i^{(l)}(0)+\sum_{r=1}^{k}(1-\xi)^{r-1}\phi_i(k-r)
\end{aligned}
\]

for all $k>0$. Since $0<\xi<1$ and $\lim_{k\to\infty}\phi_i(k)=0$, it holds that

\[
\begin{aligned}
\lim_{k\to\infty}z_i^{(l)}(k+1)
&=\lim_{k\to\infty}\left[(1-\xi)^kz_i^{(l)}(0)+\sum_{r=1}^{k}(1-\xi)^{r-1}\phi_i(k-r)\right]\\
&=0.
\end{aligned}
\]

The proof is completed.

Given any $H_l>0$, we define

\[
S(H_l)=\{w_l\mid \|w_l\|\leq H_l\}.
\]