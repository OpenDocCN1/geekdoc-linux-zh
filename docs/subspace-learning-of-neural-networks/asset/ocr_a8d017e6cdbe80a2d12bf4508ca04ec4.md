If $w(k)\ge 1+1/(2\eta)$, it holds that

$$2\eta w^2(k)-w(k)-2\eta-1\ge 0.$$

Then

$$|w(k+1)|=w^2(k)-\frac{2\eta w^2(k)-2\eta-1}{w(k)}\ge w^2(k).$$

$w(k)$ will clearly tend to infinity if $w(k)\ge 1+1/(2\eta)$. So, an important problem to address is whether an invariant set can be obtained to guarantee the nondivergence. This is a crucial problem to address to ensure the success of applications.

# **Lemma 2.7** Suppose that $\eta\sigma\le 0.25$ and $0<\|w(k)\|^2\le 1+\frac{1}{2\sigma\eta}$, then

$$1+\eta\bigl(\lambda_i(2-\|w(k)\|^2)-w^T(k)Cw(k)\bigr)>0,\qquad (i=1,\ldots,n)$$

$for\ all\ k\ge 0.$

*Proof:* Given any $i(1\le i\le n)$, if $2\le\|w(k)\|^2<1+1/(2\eta\sigma)$, then

$$1+\eta\bigl(\lambda_i(2-\|w(k)\|^2)-w^T(k)Cw(k)\bigr)\ge 1+\eta\bigl(\sigma(2-\|w(k)\|^2)-\sigma\|w^T\|^2\bigr)>0,$$

for all $k\ge 0$. If $\|w(k)\|^2<2$, then

$$1+\eta\bigl(\lambda_i(2-\|w(k)\|^2)-w^T(k)Cw(k)\bigr)\ge 1-w^T(k)Cw(k)\ge 1-2\eta\sigma>0,$$

for all $k\ge 0$. The proof is completed.

# **Theorem 2.4** Denote

$$S=\left\{w(k)\mid w(k)\in\mathbb{R}^n,\ \|w(k)\|^2\le 1+\frac{1}{2\sigma\eta}\right\}.$$

$$\eta\sigma\le 0.25,$$

then $S$ is an invariant set of $(2.12)$.

*Proof:* From Lemma 2.7, if $2\le\|w(k)\|^2\le 1+\frac{1}{2\sigma\eta}$, then

$$0<1+\eta\bigl(\lambda_i(2-\|w(k)\|^2)-w^T(k)Cw(k)\bigr)<1,\qquad (i=1,\ldots,n)$$

for $k\ge 0$. From (1.7), (2.13), it follows that

$$\begin{aligned}
\|w(k+1)\|^2
&=\sum_{i=1}^{n}\left[1+\eta\bigl(\lambda_i(2-\|w(k)\|^2)-w^T(k)Cw(k)\bigr)\right]^2z_i^2(k)\\
&\le \left[1+\eta\bigl(\lambda_p(2-\|w(k)\|^2)-w^T(k)Cw(k)\bigr)\right]^2\|w(k)\|^2\\
&\le 1+\frac{1}{2\sigma\eta}.
\end{aligned}$$