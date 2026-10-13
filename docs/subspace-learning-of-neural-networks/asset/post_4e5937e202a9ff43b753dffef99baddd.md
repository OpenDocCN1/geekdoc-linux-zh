
![](img/5d1bf22d32ba379cbf31221a5347fdb6_34_0.png)

**FIGURE 1.5**  
The original picture of Lenna (left), and the picture divided into 4096 blocks (right).

data, it can accelerate the convergent speed and reduce the oscillation of the algorithm. Generally, we set \(\beta = 1\) if \(\{x(k)\}\) comes from a stationary process. In simulations, signal-to-noise ratio (SNR) is calculated to measure the quality of image compression as

$$\mathrm{SNR}=10\log_{10}\frac{\displaystyle\sum_{i=1}^{\mathrm{row}}\sum_{j=1}^{\mathrm{col}} I_{ij}^{2}}{\displaystyle\sum_{i=1}^{\mathrm{row}}\sum_{j=1}^{\mathrm{col}}(I_{ij}-\hat{I}_{ij})^{2}}. \tag{1.11}$$

where \(I_{ij}, \hat{I}_{ij}\) represent the pixel of original image or reconstructed image, respectively.

### 1.5 Conclusion

This chapter first provides a brief introduction to linear neural networks and subspace learning algorithms of neural networks. Then, the DCT method and DDT method for convergence analysis are introduced. It can be seen that DDT method is a more reasonable approach for indirectly studying the original SDT algorithm. At the same time, the relationship between a SDT algorithm and the corresponding DDT algorithm is given. Finally, some notations and preliminaries are presented. This chapter lays the foundation for subsequent chapters.

## 2 PCA Learning Algorithms with Constant Learning Rates

### 2.1 Introduction

Principal component analysis (PCA) neural networks are useful tools in feature extraction, data compression, pattern recognition, and time series prediction, especially in online data processing applications. The learning algorithms of PCA neural networks play an important role in their practical applications. Stemming from Oja’s algorithm [134], many PCA algorithms have been proposed to update the weights of these networks. Among the algorithms for PCA, Oja’s algorithm and Xu’s LMSER algorithm are commonly used in practical applications. Several other algorithms for PCA are related to the two basic procedures [32]. In this chapter, we will study the Oja’s and Xu’s algorithms and establish the theoretical foundation of their applications.

The convergence of the learning algorithms determines whether these applications can be successful. This chapter proposes a convergence analysis framework, called DDT method, to study the convergence of Oja’s and Xu’s algorithms with constant learning rates. The original SDT algorithms are first transformed into the corresponding DDT algorithms. Then, local non-divergence conditions are guaranteed by using the invariant sets. Finally, in the invariant sets, the local convergence properties of the DDT algorithms are discussed via Cauchy principle, inequalities analysis method, and so on.

This chapter is organized in three parts. The first part¹ analyzes the convergence of Oja’s algorithm with a constant learning rate via DDT method. In Section 2.2.1, we will briefly discuss the Oja’s PCA learning algorithm and the traditional DCT method. Some preliminaries and the DDT formulation will be presented in Section 2.2.2. In Section 2.2.3, invariant sets and convergence will be studied. Simulation results and discussions will be provided in Section 2.2.4. Finally, conclusions will be drawn in Section 2.2.5.

The second part of the chapter discusses the convergence of Xu’s LMSER algorithms with a constant learning rate. Section 2.3.1 describes the formulation and preliminaries. In Sections 2.3.2 and 2.3.3, the convergence results are obtained. An invariant set and an ultimate bound are derived. A mathematical proof is given to prove the convergence. Simulation results and discussions will be provided in Section 2.3.4. Conclusions are drawn in Section 2.3.5.

The third part of the chapter compares the convergent properties of Oja’s algorithm with Xu’s LMSER’s. The chapter concludes in Section 2.5.

### 2.2 Preliminaries

Let \(C=\mathbb{E}[x(k)x^T(k)]\). Suppose that \(\lambda_p\) is the smallest nonzero eigenvalue; that is, \(\lambda_p>0\) but \(\lambda_j=0\) \((j=p+1,\ldots,n)\). Denote by \(\sigma\), the largest eigenvalue of \(C\). Suppose that the multiplicity of \(\sigma\) is \(m(1\leq m\leq p\leq n)\), then,

$$\sigma=\lambda_1=\cdots=\lambda_m.$$

Suppose that \(\{v_i\mid i=1,\ldots,n\}\) is an orthonormal basis in \(\mathbb{R}^n\) such that each \(v_i\) is a unit eigenvector of \(C\) associated with the eigenvalue \(\lambda_i\). Denote by \(V_\sigma\) the eigensubspace of the largest eigenvalue \(\sigma\); that is,

$$V_\sigma=\operatorname{span}\{v_1,\ldots,v_m\}.$$

Denoting by \(V_\sigma^\perp\) the subspace, which is perpendicular to \(V_\sigma\), clearly,

$$V_\sigma^\perp=\operatorname{span}\{v_{m+1},\ldots,v_n\}.$$

The following lemma will be useful in this chapter.

**Lemma 2.1** *It holds that*

$$[1+\eta(\sigma-s)]^2s\leq\frac{4}{27\eta}(1+\eta\sigma)^3$$

*for all \(s\in[0,\sigma+1/\eta]\).*

*Proof:* Define a differentiable function

$$f(s):=[1+\eta(\sigma-s)]^2s$$

for \(0\leq s\leq\sigma+1/\eta\). It follows that

$$\dot{f}(s)=[1+\eta(\sigma-s)]\cdot[1+\eta(\sigma-3s)]$$

for \(0\leq s\leq\sigma+1/\eta\). Denote

$$\xi=\frac{1}{3}\left(\sigma+\frac{1}{\eta}\right).$$

Then,

$$
\dot{f}(s)=
\begin{cases}
>0, & \text{if } 0\le s<\xi,\\
=0, & \text{if } s=\xi,\\
<0, & \text{if } \xi<s<\sigma+1/\eta,\\
=0, & \text{if } s=\sigma+1/\eta.
\end{cases}
$$

This shows that \(\xi\) must be the maximum point of the function \(f(s)\) on the interval \([0,\sigma+1/\eta]\). Then, it holds that

$$
f(s)\le f(\xi)=\frac{4}{27\eta}(1+\eta\sigma)^3,
$$

for all \(0\le s\le \sigma+1/\eta\). The proof is completed.

### 2.3 Oja’s Algorithm

In 1982, Oja used a simple linear single neural network in Figure 1.1 to extract the first principal component from the input data [134]. Based on the well-known Hebbian learning rule, Oja proposed a principal component analysis (PCA) learning algorithm to update the weights of the network. This network, under Oja’s algorithm, is able to extract a principal component from input data adaptively. The results have been useful in online data processing applications.

In [210], Zufiria proposed to study the dynamical behaviour of Oja’s learning algorithm by analyzing a related DDT algorithm. Certain local and global dynamical properties of DDT algorithm have been reported in [210]. Zufiria has shown that some trajectories of the DDT algorithm can be divergent and even chaotic in nature. Certain local stability results have also been reported. Following the DDT algorithm approach of [210], a generalized Oja’s PCA learning algorithm, called bounded PCA algorithm, has been studied in [202].

An important problem to now address – Is the corresponding DDT algorithm of Oja’s algorithm in [210] convergent? Since the work of [210], clearly, the DDT algorithm has not been shown to be convergent globally. Moreover, some trajectories may diverge and even become chaotic. Thus, it is quite interesting to explore whether there exists invariant sets to retain the trajectories within the sets and shed some invariant sets to explore the bigger issue of convergence. This section will study these problems in details. The DDT algorithm has many equilibria and thus the study of convergence belongs to a multistability problem. Multistability analysis has recently received attractive attentions, see, for examples, [194], [191], [192], [193]. Novel and deep results regarding convergence of the DDT algorithm will be discussed in this section. A large number of invariant sets will be involved. Any trajectory of the DDT algorithm starting from an invariant set will remain in it indefinitely. This is interesting because it provides a method to avoid divergence of the DDT algorithm by selecting a proper initial vector of the DDT algorithm from the invariant set. Moreover, the convergence of the DDT algorithm can now be proved. In the next section, we will show that almost all trajectories of the DDT algorithm starting from an invariant set will converge to an eigenvector associated with the largest eigenvalue of the correlation matrix. Consequently, it confirms that one can use a constant learning rate in Oja’s PCA learning algorithm to guarantee convergence if initial vectors are suitably chosen.

#### 2.3.1 Oja’s Algorithm and the DCT Method

With the network (1.1) and input sequence (1.2), the basic Oja’s PCA learning algorithm for weight updating is described as

$$w(k+1)=w(k)+\eta y(k)[x(k)-y(k)w(k)], \qquad (2.1)$$

for \(k \ge 0\), where \(\eta(k)>0\) is the learning rate.

It is very difficult to study the convergence of (2.1) directly. To indirectly interpret the convergence of (2.1), traditionally, the DCT method is used. This method can be simply described as follows: applying a fundamental stochastic approximation theorem [117] to (2.1), a deterministic continuous time system can be obtained:

$$\frac{dw(t)}{dt}=Cw(t)-w^T(t)Cw(t)\cdot w(t),\qquad t\ge 0,$$

where \(C=\mathbb{E}\,[x(k)x^T(k)]\) denotes the covariance matrix of

$$\{x(k)\mid x(k)\in\mathbb{R}^n(k=0,1,2,\ldots)\}.$$

The convergence of this DCT system is then used to interpret the convergence of (2.1). To transform (2.1) into the above DCT system, the following restrictive conditions are required:

-   (C1): \(\sum_{k=0}^{+\infty}\eta^2(k)<+\infty\);
-   (C2): \(\sup_k\mathbb{E}\{[y(k)\,[x(k)-y(k)w(k)]]^2\}<+\infty\).

By the condition (C1), clearly, it implies that \(\eta(k)\to 0\) as \(k\to+\infty\). However, in many practical applications, \(\eta(k)\) is often set to a small constant due to the round-off limitation and speed requirement [210, 201]. The condition (C2) is also difficult to be satisfied [210]. Thus, these conditions are unrealistic in practical applications, and the previous DCT analysis is not directly applicable [210], [201].

#### 2.3.2 DDT Formulation

To overcome the problem of learning rate converging toward zero, a DDT method is proposed in [210]. Unlike the DCT method to transform (2.1) into a continuous time deterministic system, the DDT method transforms
