for all $k>K_l$. It follows that

$$
\begin{aligned}
\|w_l(k+1)\|^2
&\ge (1-\xi)^2\|w_l(k)\|^2
+\xi^2\frac{w_l^T(k)\tilde C_l(k)\tilde C_l^T(k)w_l(k)}{[w_l^T(k)\tilde C_l(k)w_l(k)]^2}\\
&=(1-\xi)^2\|w_l(k)\|^2+\xi^2\frac{\tilde\Lambda}{\lambda_1\|w_l(k)\|^2}\\
&\ge 2\xi(1-\xi)\sqrt{\frac{\tilde\Lambda}{\lambda_1}}.
\end{aligned}
$$

for $k\ge K_l$, where $\tilde\Lambda=\min\{\Lambda_{\min}^{(l)}(k),\,k>0\}$.

Since $0<\xi<1$, from the assumption A3 and (4.14), it follows that

$$
\begin{aligned}
\|w_l(k+1)\|
&\le (1-\xi)\|w_l(k)\|+\xi\frac{M_l}{\lambda_p\|w_l(k)\|}\\
&=(1-\xi)^k\|w_l(0)\|+\xi\frac{M_l}{\lambda_p}\sum_{i=1}^{k}\frac{(1-\xi)^{i-1}}{\|w_l(k-i)\|}\\
&\le (1-\xi)^k\|w_l(0)\|+\xi\tilde H_l\sum_{i=1}^{k}(1-\xi)^{i-1}\\
&\le \tilde H_l.
\end{aligned}
$$

for $k\ge K_l$, where $\tilde H_l=\dfrac{M_l}{\lambda_p\sqrt{2\xi(1-\xi)\sqrt{\frac{\tilde\Lambda}{\lambda_1}}}}$. The proof is completed.

This lemma requires $w_l(k)\neq V_0^{(l)}(k)$ for all $k\ge 0$. This condition can be usually satisfied. It is because $\tilde C_l(k)$ will change with time and $V_0^{(l)}(k)$ is only a varying subspace. However, $l\le p$ so that $\tilde C_l(k)$ may not converge to zero with time.