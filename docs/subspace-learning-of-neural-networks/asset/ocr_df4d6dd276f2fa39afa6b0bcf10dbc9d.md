It is easy to see why the stochastic input has a great influence on the result of DDT method. Thus, obtaining the invariant set of the original SDT algorithm is a good solution to the problem. Chapter 6 explains this problem in detail.

# 1.4  Some Notations and Preliminaries

# 1.4.1  Covariance Matrix

For the input sequence (1.2), let $C = E[x(k)x^T(k)]$. It is known that the covariance matrix $C$ is a symmetric nonnegative definite matrix. There exists an orthonormal basis of $R^n$ composed by eigenvectors of $C$. Let $λ_1, …, λ_n$ be all the eigenvalues of $C$, ordered by $λ_1 ≥ … ≥ λ_n ≥ 0$. Suppose that ${v_i | i = 1, …, n}$ is an orthonormal basis in $R^n$ such that each $v_i$ is a unit eigenvector of $C$ associated with the eigenvalue $λ_i$.

For each $k ≥ 0$, $w(k) ∈ R^n$ can be represented as

$$w(k)=\sum_{i=1}^{n}z_i(k)v_i,$$  (1.7)

where $z_i(k)(i = 1, …, n)$ are some constants, and then

$$Cw(k)=\sum_{i=1}^{n}λ_i z_i(k)v_i=\sum_{i=1}^{p}λ_i z_i(k)v_i.$$  (1.8)

# 1.4.2  Simulation Data

The well-known gray picture of Lenna in Figure 1.5 (left) will be often used for simulations in this book. The 512 × 512 pixel image is decomposed into 4096 blocks that do not intersect one another, as shown in Figure 1.5 (right). Each block comprises 8 × 8 pixels, which constructs a 64-dimensional vector. Thus, a vector set with 4096 vectors is obtained. Upon removal of the mean and normalization, randomly selected vectors from this vector set form an input sequence

$\{x(k)|x(k) ∈ R^{64}, (k = 1, 2, 3, …)\}$.  (1.9)

To cater to the tracking capability of the adaptive algorithm, we will often use $C_k$ to replace $x(k)x^T(k)$ in (1.4); the $C_k$ is defined as follows [32, 31]:

$$C_k=βC_{k−1}+\frac{1}{k}\left(x(k)x^T(k)−βC_{k−1}\right),\quad (k ≥ 0).$$  (1.10)

where $β$ is a forgetting factor, which ensures that the past data samples are down-weighted. Since each $C_k$ contains some history information of the input