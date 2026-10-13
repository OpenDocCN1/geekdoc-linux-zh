This chapter is organized as follows. The traditional MCA method is reviewed, and the improved Oja+’s MCA neural network is presented in Section 2. In Section 3, we propose a method of multi-block-based MCA neural network. Some simulation results will be given to illustrate the effectiveness and accuracy of the proposed method in Section 4. Finally, in Section 5, the conclusion follows.

# 9.2  MCA Method

# 9.2.1  Matrix Algebraic Approaches

Let $X=\{x(k)|x(k)\in R^n(k=0,1,2,\ldots)\}$ be an $n$-dimensional zero-mean, Gaussian stationary data set with the nonnegative definite covariance matrix $C=E\{x(k)x^T(k)\}$. Let $\lambda_i$ and $w_i$ $(i=1,\ldots,n)$ denote the eigenvalues and the corresponding eigenvectors of $C$, respectively. We shall arrange the orthonormal eigenvectors such that the corresponding eigenvalues are in a nondecreasing order: $0<\lambda_1\leq\lambda_2\leq\cdots\leq\lambda_n$, then $w_i^Tx$ is the $i$th smallest minor component, where $1\leq i\leq n$ is the corresponding eigenvector to $\lambda_i$. To obtain the eigenvectors and eigenvalues, we can either apply eigen decomposition to the covariance matrix or the data matrix or directly apply SVD to the data matrix.

Applying SVD, we can get

$$X=UDV^T$$

in which, $U$’s columns are eigenvectors of $XX^T$, and $V$’s columns are eigenvectors of $X^TX$, while $D$ is a diagonal matrix with the diagonal elements $d_i$, the singular values, which are the square roots of the eigenvalues of $X^TX$.

# 9.2.2  Improved Oja+’s MCA Neural Network

In [135], Oja proposed to use a linear neural network in Figure 1.5 for computing the minor component of the covariance matrix associated with a given stochastic data set. The Oja+’s MCA learning algorithm can be described by the following stochastic difference equations:

$$\begin{aligned} w(k+1)={}&w(k)-\eta(k)[C_k w(k)\\ &\quad-w^T(k)C_k w(k)w(k)\\ &\quad+\mu(\|w(k)\|^2-1)w(k)], \end{aligned} \tag{9.1}$$

where $\mu$ is a constant and $\eta(k)>0$, $\eta(k)\to 0$, and $C_k=x(k)x^T(k)$ is an online observation of the covariance matrix defined by $C=E\{x(k)x^T(k)\}$. To afford the tracking capability of the adaptive algorithm, the online observation $C_k$ in (1.10) is used.