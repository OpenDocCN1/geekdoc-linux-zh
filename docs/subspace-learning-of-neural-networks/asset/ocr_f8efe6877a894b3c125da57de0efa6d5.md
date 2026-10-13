for η(k) > 0. The algorithm (2.11) approximates the Oja’s one unit rule when the normal of weight vector approaches one [184]. However, it shows some different dynamical behaviors. In this chapter, by studying an associated DDT algorithm, we will discuss the convergence of (2.11), which is a special case of the one unit version of Xu’s LMSER algorithm. By taking the conditional expectation E{w(k + 1)/ω(0), w(i), i < k}, the DDT algorithm of (2.11) with a constant learning rate is given as follows:

$$w(k+1)=w(k)+\eta\left[2Cw(k)-C(k)w(k)w^T(k)w(k)-\left(w^T(k)Cw(k)\right)w(k)\right]. \tag{2.12}$$

for η > 0 and C = E[x(k)xᵀ(k)] is the covariance matrix.

From (1.7), (1.8), (2.12), it holds that

$$z_i(k+1)=\left[1+\eta\left(\lambda_i(2-\|w(k)\|^2)-w^T(k)Cw(k)\right)\right]z_i(k), \tag{2.13}$$

for k ≥ 0, where i = 1, …, n.

**Definition 2.2** A point w* ∈ Rⁿ is called an equilibrium of (2.12), if and only if

$$w^*=w^*+\eta\left[2Cw^*-Cw^*(w^*)^Tw^*-\left((w^*)^TCw^*\right)w^*\right].$$

Clearly, the set of all equilibrium points of (2.12) is

$$\{\text{all the eigenvectors with unit length}\}\cup\{0\}.$$

**Definition 2.3** A bound M is called an ultimate bound of (2.12), if for any w(0) ∈ S, there exists a constant N so that ‖w(k)‖² < M for all k ≥ N.

For convenience in analysis, a lemma is presented as follows.

**Lemma 2.6** It holds that

$$\left[1+\eta\left(\sigma(2-s)\right)\right]^2s\leq\frac{4}{27\eta\sigma}\cdot(1+2\eta\sigma)^3$$

for all s ∈ [0, 2 + 1/ησ].

It is easy to prove this lemma by Lemma 2.1

# 2.4.2  Invariant Set and Ultimate Bound

The system (2.12) is not globally convergent. Consider the same example as in Section 3, which is the one-dimensional case,

$$w(k+1)=w(k)+\eta\left[2-2w^2(k)\right]w(k),\quad \text{for } k\geq 0.$$