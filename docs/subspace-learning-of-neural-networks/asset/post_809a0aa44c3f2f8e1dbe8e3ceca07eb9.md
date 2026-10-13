
cardiogram (FECG). Theoretical analysis of the algorithm is also given in this chapter.

Finally, in Chapter 11, a rigid medical image registration method is introduced. The proposed method accomplishes registration by simply aligning the first principal component direction and centroids of feature images. Since a PCA neural network is used to compute the first principal component direction of feature images, the registration is simple and efficient.

## 1.2 Methods for Convergence Analysis

The learning algorithms of neural networks play an important role in their practical applications. The convergence of learning algorithms determines whether these applications can be successful. However, it is very difficult to directly study the convergence of these learning algorithms, because they are described by stochastic discrete time (SDT) algorithms [202]. Generally, two methods are used to analyze the convergence of learning algorithms. Traditionally, based on some stochastic approximation theorems [14, 35, 117], an original SDT algorithm is transformed into a corresponding deterministic continuous time (DCT) algorithm. The convergence of the SDT algorithm can be indirectly interpreted by studying the corresponding DCT algorithm. This approach is called the DCT method. Another method is called the deterministic discrete time (DDT) method. The DDT method transforms a SDT algorithm into a corresponding DDT algorithm by taking the conditional expectation on both sides of the SDT algorithm. The DDT algorithm characterizes the average evolution of the original SDT algorithm. The DDT algorithm preserves the discrete time nature of the original algorithm. The convergence of the DDT algorithm can shed some light on the dynamical behaviors of the original SDT algorithm.

### 1.2.1 DCT Method

Traditionally, based on some stochastic approximation theorems [14, 117], an original SDT algorithm is transformed into a corresponding deterministic continuous time (DCT) algorithms; that is, the algorithm (1.4) is transformed into the following differential equation (1.5):

$$\dot{w}(k) = \Delta w(k) \tag{1.5}$$

The convergence of the algorithm (1.4) can be indirectly interpreted by studying the corresponding DCT algorithm (1.5). Because of mathematical achievements of the differential equation, the method has been widely used; see for examples, [4, 36, 135, 136, 154, 162, 172, 192, 199].

In order to transform an SDT algorithm to a DCT algorithm, some restrictive conditions must be applied. One of these conditions is that

\[\eta(k)>0,\quad \sum_k \eta(k)=\infty,\quad \sum_k(\eta(k))^2<\infty.\]

where \(\eta(k)\) is the learning rate of the SDT learning algorithm (1.4). This condition implies that the learning rate \(\eta(k)\) must converge to zero. However, it is unrealistic in practical applications, because of computational round-off limitations and tracking requirements, whenever the step increases considerably. If small but nonzero constant values of learning rate have to be employed [210]. If the learning rate approaches zero, it could slow down the convergent speed of the algorithm considerably. In addition, the learning rate cannot approach zero too fast; otherwise, the algorithm will stop before it converges to the right direction. More discussions can be found in [39, 195, 202, 210]. Thus, the condition above is unrealistic in practical applications.

### 1.2.2 DDT Method

To overcome the shortcomings of the DCT method, the deterministic discrete time (DDT) method has been proposed recently to indirectly study the convergence of SDT learning algorithms; see [39, 124, 195, 210]. The DDT method transforms the SDT algorithm (1.4) into the corresponding DDT algorithm as follows:

\[E\{w(k+1)\}=E\{w(k)\}+E\{\eta(k)\Delta w(k)\}.\tag{1.6}\]

Then, to guarantee the nondivergence of DDT algorithms, the boundedness of the algorithms must be analyzed firstly. For global convergent algorithms, global boundedness is studied. For local convergent algorithms, invariant sets are obtained to guarantee the local nonconvergence. The invariant set is defined as follows.

**Definition 1.6** A compact set \(S\subset R^n\) is called an invariant set of the algorithm \(w(k+1)=f(w(k),x(k))\), if for any \(w(0)\in S\), the trajectory of the algorithm starting from \(w(0)\) will remain in \(S\) for all \(k \geq 0\).

An invariant set is interesting because it provides a method to guarantee nondivergence of an algorithm. Clearly, a subset of an invariant set may be not an invariant set. If a set has an invariant subset, it does not imply this set is also an invariant set [195].

Under the conditions of nondivergence, Cauchy convergence principle, inequalities analysis method, and so on, are used to derive the convergence conditions and rigorously prove the convergence of algorithms. The results can shed some light on the original algorithms.

The DDT method does not require the learning rates to converge to zero so that constant learning rates can be used. The DDT algorithms preserve the discrete time nature of the original algorithms and allow a more realistic dynamic behavior of the learning rates [210]. Compared to the DCT method, the DDT method is a more reasonable approach for indirectly studying the convergence of SDT algorithms.

The DDT algorithm characterizes the average evolution of the original SDT algorithm. In a stochastic environment, the stochastic input has a great influence on the result of DDT method, even derailing the convergent conditions of the DDT algorithm [120]. In Chapter 6, we propose a method to avoid this issue. First, nondivergence of an original algorithm is guaranteed in stochastic environment by directly studying the original algorithm. Under this condition, convergence of the algorithm is analyzed via DDT method.

## 1.3 Relationship between SDT Algorithm and DDT Algorithm

The SDT algorithm (1.4) and the corresponding DDT algorithm (1.6) all preserve the discrete time nature. The DDT algorithm (1.6) can also be presented as

$$\frac{1}{L}\sum_{i=1}^{L}\{w(k+1)\}=\frac{1}{L}\sum_{i=1}^{L}\{w(k)\}\pm\frac{1}{L}\sum_{i=1}^{L}\{\eta(k)\Delta w(k)\},\ L\to\infty.$$

Clearly, if $L=1$, this is the SDT algorithm (1.4). Thus, let $L$ be some constants. We have got some algorithms called block algorithms. The block algorithms not only establish a relationship between an original SDT algorithm and the corresponding DDT algorithm, as shown in Figure 1.4, but also get a compromise between the SDT algorithm and the DDT algorithm.

![](img/5d1bf22d32ba379cbf31221a5347fdb6_32_0.png)

**FIGURE 1.4**  
Relationship between SDT algorithm and DDT algorithm.

The block size $L$ plays an important role in the block algorithms, which can be determined according to the practical applications [129]. For an SDT algorithm and the corresponding block algorithms and DDT algorithm, it is easy to get the following result.

**Corollary 1.1**  *The invariant sets of an original SDT algorithm are also the invariant sets of the corresponding block algorithms and DDT algorithm, but not vice versa.*

It is easy to see why the stochastic input has a great influence on the result of DDT method. Thus, obtaining the invariant set of the original SDT algorithm is a good solution to the problem. Chapter 6 explains this problem in detail.

## 1.4 Some Notations and Preliminaries

### 1.4.1 Covariance Matrix

For the input sequence (1.2), let $C = E[x(k)x^T(k)]$. It is known that the covariance matrix $C$ is a symmetric nonnegative definite matrix. There exists an orthonormal basis of $R^n$ composed by eigenvectors of $C$. Let $λ_1, …, λ_n$ be all the eigenvalues of $C$, ordered by $λ_1 ≥ … ≥ λ_n ≥ 0$. Suppose that ${v_i | i = 1, …, n}$ is an orthonormal basis in $R^n$ such that each $v_i$ is a unit eigenvector of $C$ associated with the eigenvalue $λ_i$.

For each $k ≥ 0$, $w(k) ∈ R^n$ can be represented as

$$w(k)=\sum_{i=1}^{n}z_i(k)v_i,$$  (1.7)

where $z_i(k)(i = 1, …, n)$ are some constants, and then

$$Cw(k)=\sum_{i=1}^{n}λ_i z_i(k)v_i=\sum_{i=1}^{p}λ_i z_i(k)v_i.$$  (1.8)

### 1.4.2 Simulation Data

The well-known gray picture of Lenna in Figure 1.5 (left) will be often used for simulations in this book. The 512 × 512 pixel image is decomposed into 4096 blocks that do not intersect one another, as shown in Figure 1.5 (right). Each block comprises 8 × 8 pixels, which constructs a 64-dimensional vector. Thus, a vector set with 4096 vectors is obtained. Upon removal of the mean and normalization, randomly selected vectors from this vector set form an input sequence

$\{x(k)|x(k) ∈ R^{64}, (k = 1, 2, 3, …)\}$.  (1.9)

To cater to the tracking capability of the adaptive algorithm, we will often use $C_k$ to replace $x(k)x^T(k)$ in (1.4); the $C_k$ is defined as follows [32, 31]:

$$C_k=βC_{k−1}+\frac{1}{k}\left(x(k)x^T(k)−βC_{k−1}\right),\quad (k ≥ 0).$$  (1.10)

where $β$ is a forgetting factor, which ensures that the past data samples are down-weighted. Since each $C_k$ contains some history information of the input
