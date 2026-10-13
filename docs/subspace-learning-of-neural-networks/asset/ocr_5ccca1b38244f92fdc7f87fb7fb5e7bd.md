The previous theorems show the trajectories of the DDT algorithms starting from the invariant sets will converge to an independent component direction with a positive kurtosis or a negative kurtosis. The results can shed some light on the dynamical behaviors of the original algorithms (6.1) and (6.2).

# 6.4  Extension of the DDT Algorithms

The DDT algorithms of the algorithms (6.1) and (6.2) can be clearly expressed as

$$E\{\mathbf{w}(k+1)\}=E\{\mathbf{w}(k)\}+\eta\left[b(\mathbf{x}(k))\{\mathbf{w}^{T}(k)\mathbf{x}(k)\}^{3}+a(1-\|\mathbf{w}(k)\|^{2})\mathbf{w}(k)\right],$$
$$E\{\mathbf{w}(k+1)\}=E\{\mathbf{w}(k)\}+\eta\left[-bE\{\mathbf{x}(k)\{\mathbf{w}^{T}(k)\mathbf{x}(k)\}^{3}\}+a(1-\|\mathbf{w}(k)\|^{2})\mathbf{w}(k)\right].$$

Let $\bar{\mathbf{w}}(k)=E\{\mathbf{w}(k)\}$, the DDT algorithms are rewritten as:

$$\bar{\mathbf{w}}(k+1)=\bar{\mathbf{w}}(k)+\eta\left[bE\{\mathbf{x}(k)(\bar{\mathbf{w}}^{T}(k)\mathbf{x}(k))^{3}\}+a(1-\|\bar{\mathbf{w}}(k)\|^{2})\bar{\mathbf{w}}(k)\right], \tag{6.10}$$
$$\bar{\mathbf{w}}(k+1)=\bar{\mathbf{w}}(k)+\eta\left[-bE\{\mathbf{x}(k)(\bar{\mathbf{w}}^{T}(k)\mathbf{x}(k))^{3}\}+a(1-\|\bar{\mathbf{w}}(k)\|^{2})\bar{\mathbf{w}}(k)\right]. \tag{6.11}$$

By studying the convergence of the DDT algorithms (6.10) and (6.11), we indirectly analyze the convergence of the original SDT algorithms (6.1) and (6.2). Clearly, the algorithms will converge under certain conditions. However, the original SDT algorithms have slow convergence speed, and convergence accuracy of these algorithms is not good [129, 197, 198]. To improve the performance of the original algorithms, the DDT algorithms can be extended to the block versions of the original algorithms. If the expectation operation is computed by

$$E\{\mathbf{x}(k)(\bar{\mathbf{w}}^{T}(k)\mathbf{x}(k))^{3}\}=\frac{1}{L}\sum_{j=1}^{L}\mathbf{x}(j)(\bar{\mathbf{w}}^{T}(j)\mathbf{x}(j))^{3},$$

where $L$ is the block size [129], the algorithms (6.10) and (6.11) are also the block algorithms. The block algorithms establish a relationship between the original SDT algorithms and the corresponding DDT algorithms. Clearly, if $L=1$, they are the original SDT algorithms. If $L$ is the size of all examples, they are the corresponding DDT algorithms. The block algorithms represent an average evolution of the original algorithms over all blocks of samples. Thus, many arrival sets in Theorem 6.1 (where $L=1$) also are the invariant sets of the block algorithms. Furthermore, the block algorithms can get a good convergence speed and accuracy in practice. The following simulations will illustrate their performance.