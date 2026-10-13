# 2.3.5  Conclusion

Important results pertaining to the convergence of a DDT algorithm of Oja’s PCA learning algorithm have been derived in this section. It shows that almost all trajectories starting from an invariant set converge to the unit eigenvector associated with the largest eigenvalue of the covariance matrix if the learning rate satisfy some simple condition. We suggest using the unit hyper-sphere for conveniently choosing the initial vector to guarantee convergence and the selection of learning rate to achieve fast convergence. Simulation studies are carried out to further illustrate the theory. The most important result is that it confirms that the use of a constant learning rate for Oja’s PCA learning algorithm can achieve convergence.

# 2.4  Xu’s LMSER Learning Algorithm

In [184], based on the least mean square error reconstruction, Xu proposed a learning algorithm to perform the true PCA. In this section, by using the DDT method, we will discuss the convergence of Xu’s LMSER algorithm, in the one unit case, with a constant learning rate. An invariant set and an evolution ultimate bound are identified. A mathematical proof will be provided to prove the convergence.

# 2.4.1  Formulation and Preliminaries

Suppose the input sequence (1.2) is a zero mean stationary stochastic process, denoted by $C = E[x(k)x^T(k)]$, the covariance matrix of the input data set, and let $C_k$ be an online observation of $C$, then the Xu’s learning algorithm can be described by the following stochastic difference equation:

$$\begin{aligned}
w_l(k+1) ={}& w_l(k)+\eta(k)[2C_kw_l(k)\\
&-\sum_{i=1}^{l-1} C_kw_i(k)w_i^T(k)w_l(k)-C_kw_l(k)w_l^T(k)w_l(k)\\
&-\sum_{i=1}^{l-1} w_i(k)w_i^T(k)C_kw_l(k)-\big(w_l^T(k)C_kw_l(k)\big)w_l(k)], \tag{2.10}
\end{aligned}$$

for $\eta(k)>0$, where $w_l$ is the input weight vector for the $l$th neuron. Obviously, if $l=1$, the algorithm is as follows:

$$w(k+1)=w(k)+\eta(k)[2C_kw(k)-C_kw(k)w^T(k)w(k)-\big(w^T(k)C_kw(k)\big)w(k)], \tag{2.11}$$