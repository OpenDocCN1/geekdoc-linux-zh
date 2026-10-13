Thus,

$$W^T(k+1)CW(k+1)\leq \frac{1}{\eta}.$$

This shows that $w(k+1)\in S$, that is, $S$ is an invariant set. The proof is completed. Next, we will provide a deeper result, which will give a family of invariant sets.

# **Theorem 2.2** Given any constant $l$ such that $1\leq l\leq 2$, if

$$\eta\sigma\leq \frac{3\sqrt[3]{2l}-2}{2},$$

then, the set

$$S(l)=\left\{w\mid w\in\mathbb{R}^n,\;w^TCw\leq \lambda_p+\frac{l}{\eta}\right\}$$

is an invariant set of (2.2).

*Proof:* Given any $k\geq 0$, suppose $w(k)\in S(l)$, we will prove that $w(k+1)\in S(l)$. Clearly,

$$0\leq w^T(k)Cw(k)\leq \lambda_p+\frac{l}{\eta}.$$

If

$$\sigma\leq w^T(k)Cw(k)\leq \lambda_p+\frac{l}{\eta},$$

then

$$\left[1+\eta\left(\lambda_i-w^T(k)Cw(k)\right)\right]^2$$
$$=1+\eta^2\left(w^T(k)Cw(k)-\lambda_i\right)\left(w^T(k)Cw(k)-\lambda_i-\frac{2}{\eta}\right)$$
$$\leq 1,\quad (i=1,\ldots,p).$$

Thus,

$$w^T(k+1)Cw(k+1)$$
$$=\sum_{i=1}^{n}\lambda_i z_i^2(k+1)$$
$$=\sum_{i=1}^{p}\lambda_i z_i^2(k+1)$$
$$=\sum_{i=1}^{p}\lambda_i\left[1+\eta\left(\lambda_i-w^T(k)Cw(k)\right)\right]^2z_i^2(k)$$
$$\leq\sum_{i=1}^{p}\lambda_i z_i^2(k)$$
$$=w^T(k)Cw(k)$$
$$\leq\lambda_p+\frac{l}{\eta}.$$