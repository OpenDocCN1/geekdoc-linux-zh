computational load compared with the second-order methods. Thus, the versatile extraction algorithms based on second-order statistics become popular.

Barros et al. [11] presented an objective function by using blind signal extraction along with prior information about the autocorrelation property of the FECG from the noisy-free measurements. We extend the work for the noisy case. Theoretical analysis of the new algorithm is also given in this chapter [111].

This chapter is organized as follows. In Section 2, problem formulation is given. A new algorithm is proposed and theoretical analysis is given in Section 3. Section 4 presents the simulations. Conclusions are drawn in Section 5.

# 10.2  Problem Formulation

Let us denote $s(k)=[s_1(k),\ldots,s_n(k)]^T$ as the source signals vector and by $x(k)=[x_1(k),\ldots,x_n(k)]^T$ as the observed signals vector. Thus, the mixture can be written as

$$x(k)=As(k)+n(k), \tag{10.1}$$

where $A$ is an $n\times n$ nonsingular matrix and $n(k)$ is additive noise. In general, the noise $n(k)$ is assumed to be uncorrelated with the source signals and its covariance matrix is given by

$$E\{n(k)n^T(k-\Delta k)\}=\begin{cases}0, & \text{for }\Delta k\neq 0\\ R_n, & \text{for }\Delta k=0\end{cases}. \tag{10.2}$$

Normally, we further assume that $R_n=\sigma_n^2I$, where $\sigma_n^2I$ is the variance of the noise. There are several approaches to estimate $\sigma_n^2$. If the number of mixtures is larger than the number of sources, we can use a subspace method to estimate $\sigma_n^2$, which in this case represents the smallest eigenvalue of $E\{x(k)x^T(k)\}$ [76], or we can use an adaptive principal component analysis method to real-time estimation of $\sigma_n^2$ [84].

We assume that the source signals have temporal structure and different autocorrelation functions, but they do not necessarily have to be statistically independent. Denote by $s_i$ the fatal heartbeat signal to extract, which satisfies the following relation for the specific time delay $\tau_i$:

$$\begin{cases}E\{s_i(k)s_i(k-\tau_i)\}\neq 0\\ E\{s_j(k)s_j(k-\tau_i)\}=0 & \forall j\neq i\end{cases}. \tag{10.3}$$

Let $y(k)=w^Tx(k)$, where $w$ is the weight vector to be estimated such that $y(k)$ recovers the specific source signal $s_i$. Define the error function as in [11]:

$$\varepsilon(k)=y(k)-by(k-\tau_i), \tag{10.4}$$