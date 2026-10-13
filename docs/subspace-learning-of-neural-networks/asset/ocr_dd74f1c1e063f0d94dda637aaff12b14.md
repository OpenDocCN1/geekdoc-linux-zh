DDT system (5.4) is an “average” of the original stochastic system (5.3). The convergence analysis results about (5.4) could reflect some “average” dynamical behaviors of (5.3).

For convenience of analysis, next, some preliminaries are given. Since the covariance matrix $C$ is a symmetric positive definite matrix, there exists an orthonormal basis of $\mathbb{R}^n$ composed of the eigenvectors of $C$. Let $\lambda_1,\ldots,\lambda_n$ be all the eigenvalues of $C$ ordered by $\lambda_1>\cdots>\lambda_n>0$. Suppose that $\{v_i\mid i=1,2,\ldots,n\}$ is an orthonormal basis of $\mathbb{R}^n$ such that each $v_i$ is a unit eigenvector of $C$ associated with the eigenvalue $\lambda_i$. Thus, for each $k\geq 0$, the weight vector $w(k)$ can be represented as

$$w(k)=\sum_{i=1}^{n}z_i(k)v_i,$$  (5.5)

where $z_i(k)\,(i=1,2,\ldots,n)$ are some constants. From (5.4) and (5.5), it holds that for all $k\geq 0$

$$z_i(k+1)=\left[1.5+(n\lambda_i-0.5)w^T(k)w(k)+n\gamma w^T(k)Cw(k)-2\eta\lambda_i\right]z_i(k),$$  (5.6)

$(i=1,2,\ldots,n)$. According to the relevant properties of the Rayleigh Quotient, it holds that

$$\lambda_n w^T(k)w(k)\leq w^T(k)Cw(k)\leq \lambda_1 w^T(k)w(k),$$  (5.7)

for all $k\geq 0$.

# 5.3  Dynamical Analysis

In this section, we study the dynamical behaviors of DDT system (5.4) via the following three steps:

+   1. **Step 1:** in Theorem 5.1, we prove that if some mild conditions are satisfied, weight vector in (5.4) is bounded.
+   2. **Step 2:** in Theorem 5.2, it is proved that weight vector in (5.4) will converge to minor component under some conditions.
+   3. **Step 3:** in Theorem 5.3, we analyze the stability of DDT system (5.4).

To analyze convergence of DDT system (5.4), we need to prove a preliminary conclusion in the following Lemma 5.1, where it is proved that under some conditions,

$$1.5+(n\lambda_i-0.5)w^T(k)w(k)+n\gamma w^T(k)Cw(k)-2\eta\lambda_i\geq 0,$$

for any $i\,(i=1,2,\ldots,n)$ in (5.6). This preliminary conclusion means that the projection of weight vector $w(k)$ on each eigenvector $v_i\,(i=1,2,\ldots,n)$, which is denoted as $z_i(k)=w^T(k)v_i\,(i=1,2,\ldots,n)$, does not change its sign in (5.6).