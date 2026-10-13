If

$$0 \leq w^T(k)Cw(k) \leq \sigma,$$

then it can be checked that

$$\begin{aligned}
[1+\eta(\lambda_i-w^T(k)Cw(k))]^2
&\leq [1+\eta(\sigma-w^T(k)Cw(k))]^2,
\end{aligned}$$

for $i=1,\ldots,n$. By Lemma 1,

$$\begin{aligned}
w^T(k+1)Cw(k+1)
&=\sum_{i=1}^{n}\lambda_i[1+\eta(\lambda_i-w^T(k)Cw(k))]^2z_i^2(k)\\
&\leq [1+\eta(\sigma-w^T(k)Cw(k))]^2\cdot w^T(k)Cw(k)\\
&\leq \max_{0\leq s\leq \sigma}\{[1+\eta(\sigma-s)]^2s\}\\
&\leq \max_{0\leq s\leq \sigma<1/\eta}\{[1+\eta(\sigma-s)]^2s\}\\
&\leq \frac{4}{27\eta}(1+\eta\sigma)^3\\
&\leq \frac{l}{\eta}\\
&\leq \lambda_p+\frac{l}{\eta}.
\end{aligned}$$

This shows that $w(k+1)\in S(l)$. The proof is completed.

Some invariant sets will follow from the above analysis. The nondivergence can thus be guaranteed by selecting initial vectors from the invariant sets. Next, we will further establish convergence results.

From (1.7), for each $k\geq 0$, $w(k)$ can be represented as

$$w(k)=\sum_{i=1}^{m}z_i(k)v_i+\sum_{j=m+1}^{n}z_j(k)v_j,$$

where $z_i(k)(i=1,\ldots,n)$ are some constants for each $k$. In particular,

$$w(0)=\sum_{i=1}^{m}z_i(0)v_i+\sum_{j=m+1}^{n}z_j(0)v_j.$$

Clearly, the convergence of $w(k)$ can be determined by the convergence of $z_i(k)(i=1,\ldots,m)$. Next, we analyze the convergence of $w(k)$ by studying the convergence of $z_i(k)(i=1,\ldots,m)$ and $z_i(k)(i=m+1,\ldots,n)$, respectively.