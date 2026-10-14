
*证明.* 定义可微函数

$$f(s)=\left[1+\frac{\xi}{s}(\sigma-s)\right]^2s$$

其中\(s>0\)。则有：

$$\dot f(s)=\left[1+\frac{\xi}{s}(\sigma-s)\right]\left[1-\frac{\xi}{s}(\sigma+s)\right]$$

其中\(s>0\)。记：

$$s^*=\frac{\xi\sigma}{1-\xi}.$$

于是，

$$\dot f(s)\begin{cases}<0, & \text{if }0<s\le s^*,\\=0, & \text{if }s=s^*,\\>0, & \text{if }s^*\le s.\end{cases}$$

这表明\(s^*\)必定是函数\(f(s)\)在区间\((0,+\infty)\)上的最小值点。因此有：

$$\left[1+\frac{\xi}{s}(\sigma-s)\right]^2s\ge 4(1-\xi)\xi\sigma,$$

对\(s>0\)成立。并且有：

$$\left[1+\frac{\xi}{s}(\sigma-s)\right]^2s\le \max\left\{\sigma,\left[1+\frac{\xi}{s_*}(\sigma-s_*)\right]^2s_*\right\}$$

对所有\(s\in[s_*,\sigma]\)成立。证明完毕。

### 3.4 带自适应学习率的Oja算法的收敛性分析

本节将系统地提供所提学习算法收敛性分析的详细内容。

#### 3.4.1 有界性

首先，我们将分析系统`(3.5)`的有界性。系统演化的下界和上界将在以下定理中给出。

**引理3.2.** 假设`0<ξ<0.8`，若`0<w^T(k)Cw(k)<λ_p`，则`w^T(k)Cw(k)`是递增的。

*证明：* 如果`w^T(k)Cw(k)≤λ_p`，可以验证：

$$\left[1+\xi\left(\frac{\lambda_i}{w^T(k)Cw(k)}-1\right)\right]^2\geq\left[1+\xi\left(\frac{\lambda_p}{w^T(k)Cw(k)}-1\right)\right]^2\geq1,$$

对于`k≥0`。然后，由`(3.5)`、`(1.7)`和`(3.6)`，我们有：

$$\begin{aligned} w^T(k+1)Cw(k+1)&=\sum_{i=1}^{p}\left[1+\xi\left(\frac{\lambda_i}{w^T(k)Cw(k)}-1\right)\right]^2\lambda_i z_i^2(k)\\ &\geq\left[1+\xi\left(\frac{\lambda_p}{w^T(k)Cw(k)}-1\right)\right]^2w^T(k)Cw(k)\\ &\geq w^T(k)Cw(k). \end{aligned}$$

对于`k≥0`。证明完毕。

**定理3.1.** 如果`w(0)∉\mathcal{V}_{\sigma}^{\perp}`，则下列不等式成立：

$$w^T(k+1)Cw(k+1)\geq4(1-\xi)\xi\lambda_p>0,$$

对所有`k≥0`成立，其中`0<ξ<0.8`。

*证明：* 可以验证：

$$\left[1+\xi\left(\frac{\lambda_i}{w^T(k)Cw(k)}-1\right)\right]^2\geq\left[1+\xi\left(\frac{\lambda_p}{w^T(k)Cw(k)}-1\right)\right]^2>0.$$

对 $k \ge 0$。由 `(3.5)`、`(1.8)` 和 `(3.6)` 可得

$$\begin{aligned}
w^T(k+1)Cw(k+1) &= \sum_{i=1}^{n}\lambda_i z_i^2(k+1)\\
&= \sum_{i=1}^{p}\lambda_i z_i^2(k+1)\\
&= \sum_{i=1}^{p}\left[1+\xi\left(\frac{\lambda_i}{w^T(k)Cw(k)}-1\right)\right]^2\lambda_i z_i^2(k)\\
&\ge \left[1+\xi\left(\frac{\lambda_p}{w^T(k)Cw(k)}-1\right)\right]^2 w^T(k)Cw(k)\\
&\ge \min_{s>0}\left\{\left[1+\xi\left(\frac{\lambda_p}{s}-1\right)\right]^2\cdot s\right\}.
\end{aligned}$$

对 $k \ge 0$。由引理 3.1，有

$$w^T(k+1)Cw(k+1)\ge 4(1-\xi)\xi\lambda_p,$$

对 $k \ge 0$。证明完毕。上述定理表明，如果 `w(0)≠0`，且从 `w(0)` 出发的轨迹有下界，则该轨迹永远不会收敛到零。显然，零向量必为 `(3.5)` 的不稳定平衡点。

**定理 3.2.** *存在常数 `H>0`，使得对所有 `k≥0` 有 `w^T(k)Cw(k)≤H`。*

*证明.* 若 `w^T(0)Cw(0)=0`，则对所有 `k≥0` 有 `w^T(k)Cw(k)=0`。显然，`w^T(k)Cw(k)≤H`。接下来，假设 `w^T(0)Cw(0)≠0`。定义

$$\bar H=\max\left\{\sigma,\left[1+\xi\left(\frac{\sigma}{\lambda_p}-1\right)\right]^2\lambda_p,\left[1+\xi\left(\frac{\sigma}{w^T(0)Cw(0)}-1\right)\right]^2w^T(0)Cw(0)\right\}.$$

给定任意正数 `H` 满足 `H≥\bar H`，我们将证明：对任意 `k≥0`，有

$$0\le w^T(k)Cw(k)\le H$$

蕴含

$$0\le w^T(k+1)Cw(k+1)\le H.$$

证明分两步完成。

**情形 1.** `σ≤w^T(k)Cw(k)≤H`。此时，

$$\left[1+\xi\left(\frac{\lambda_i}{w^T(k)Cw(k)}-1\right)\right]^2\le 1,\quad (i=1,\ldots,p).$$

因此

$$\begin{aligned} w^T(k+1)Cw(k+1) &= \sum_{i=1}^{n}\lambda_i z_i^2(k+1) \\ &= \sum_{i=1}^{p}\lambda_i z_i^2(k+1) \\ &= \sum_{i=1}^{p}\lambda_i\left[1+\xi\left(\frac{\lambda_i}{w^T(k)Cw(k)}-1\right)\right]^2z_i^2(k) \\ &\leq \sum_{i=1}^{p}\lambda_i z_i^2(k) \\ &= w^T(k)Cw(k) \\ &\leq H. \end{aligned}$$

**情形 2.** `0≤w^T(k)Cw(k)≤σ`。可以验证

$$\left[1+\xi\left(\frac{\lambda_i}{w^T(k)Cw(k)}-1\right)\right]^2\leq\left[1+\xi\left(\frac{\sigma}{w^T(k)Cw(k)}-1\right)\right]^2,$$

对 `i=1,\ldots,n`。因此

$$\begin{aligned} w^T(k+1)Cw(k+1) &= \sum_{i=1}^{p}\lambda_i\left[1+\xi\left(\frac{\lambda_i}{w^T(k)Cw(k)}-1\right)\right]^2z_i^2(k) \\ &\leq \sum_{i=1}^{p}\lambda_i\left[1+\xi\left(\frac{\sigma}{w^T(k)Cw(k)}-1\right)\right]^2z_i^2(k) \\ &= \left[1+\xi\left(\frac{\sigma}{w^T(k)Cw(k)}-1\right)\right]^2w^T(k)Cw(k) \\ &\leq \max_{0\leq s\leq\sigma}\left\{\left[1+\xi\left(\frac{\sigma}{s}-1\right)\right]^2s\right\}. \end{aligned}$$

如果

$$\lambda_p>s^*=\frac{\xi\sigma}{1-\xi},$$

由引理 3.1 和引理 3.2，可得
