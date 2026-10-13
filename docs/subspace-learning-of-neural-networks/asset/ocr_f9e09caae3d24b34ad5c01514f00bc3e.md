# **Theorem 2.1** Denote

$$S=\left\{w\mid w\in\mathbb{R}^n,\ w^T Cw\leq\frac{1}{\eta}\right\}.$$

If

$$\eta\sigma\leq\frac{3\sqrt[3]{2}-2}{2}\approx 0.8899,$$

then $S$ is an invariant set of (2.2).

**Proof:** Given any $k\geq 0$, suppose $w(k)\in S$, that is,

$$0\leq w^T(k)Cw(k)\leq\frac{1}{\eta}.$$

Then,

$$1+\eta\left(\lambda_i-w^T(k)Cw(k)\right)\geq\eta\lambda_i\geq 0,\quad(i=1,\ldots,n).$$

From (2.2), (1.7), (1.8), and (2.3), it follows that

$$\begin{aligned}
w^T(k+1)Cw(k+1)
&=\sum_{i=1}^{n}\lambda_i z_i^2(k+1)\\
&=\sum_{i=1}^{n}\lambda_i\left[1+\eta\left(\lambda_i-w^T(k)Cw(k)\right)\right]^2z_i^2(k)\\
&\leq\sum_{i=1}^{n}\lambda_i\left[1+\eta\left(\sigma-w^T(k)Cw(k)\right)\right]^2z_i^2(k)\\
&=\left[1+\eta\left(\sigma-w^T(k)Cw(k)\right)\right]^2w^T(k)Cw(k)\\
&\leq\max_{0\leq s\leq 1/\eta}\left\{\left[1+\eta(\sigma-s)\right]^2\cdot s\right\}\\
&\leq\max_{0\leq s\leq\sigma+1/\eta}\left\{\left[1+\eta(\sigma-s)\right]^2\cdot s\right\}.
\end{aligned}$$

Using Lemma 2.1,

$$w^T(k+1)Cw(k+1)\leq\frac{4}{27\eta}(1+\eta\sigma)^3.$$

By

$$\eta\sigma\leq\frac{3\sqrt[3]{2}-2}{2},$$

it follows that

$$\frac{4}{27\eta}(1+\eta\sigma)^3\leq\frac{1}{\eta}.$$