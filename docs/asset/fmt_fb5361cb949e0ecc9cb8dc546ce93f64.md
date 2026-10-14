
### 情况3：`|z_n(k_0)|>1`，且存在正整数`M` (`M>k_0`)，使得`|z_n(M)|≤1`。

由于`|z_n(M)|≤1`，与情况1类似，可以证明当`k→∞`时，`|z_n(k)|`必收敛到平衡点1。

由前面三种情况的分析，我们可以得到

$$\lim_{k\to\infty}|z_n(k)|=1. \tag{5.26}$$

同时，由(5.22)和(5.23)，我们有：若`z_n(k_0)≥0`，则对所有`k>k_0`，`z_n(k)>0`；若`z_n(k_0)≤0`，则对所有`k>k_0`，`z_n(k)≤0`。因此，由(5.26)可得

$$\lim_{k\to\infty}z_n(k)=\pm 1.$$

证毕。

在引理5.3中，我们已证明：若`ηλ_1<0.25`，`w(0)∈S`且`w^T(0)v_n≠0`，则

$$\lim_{k\to\infty}z_i(k)=0,\quad (i=1,2,\ldots,n-1). \tag{5.27}$$

在引理5.4中，证明了若`ηλ_1<0.25`，`w(0)∈S`且`w^T(0)v_n≠0`，则

$$\lim_{k\to\infty}z_n(k)=\pm 1. \tag{5.28}$$

由于

$$w(k)=\sum_{i=1}^{n-1}z_i(k)v_i+z_n(k)v_n,$$

由(5.27)和(5.28)，我们很容易得出以下结论：

### 定理5.2
*若`ηλ_1<0.25`，`w(0)∈S`且`w^T(0)v_n≠0`，则在(5.4)中，*

$$\lim_{k\to\infty}w(k)=\pm v_n.$$

至此，我们完成了DDT系统(5.4)收敛性的证明。接下来，我们进一步研究(5.4)的稳定性。显然，(5.4)的所有平衡点集合为

$$\{v_1,\ldots,v_n\}\cup\{-v_1,\ldots,-v_n\}\cup\{0\}.$$

下面的定理5.3将说明(5.4)中平衡点`v_n`和`-v_n`的稳定性。

### 定理5.3
*在`ηλ_1<0.25`的条件下，平衡点`v_n`和`-v_n`是局部渐近稳定的。*

$$\eta\lambda_1<0.25.$$

*其他平衡点是不稳定的。*

**证明.** 记

```
G(w)=w(k+1)
    =w(k)+η[(w^T(k)w(k)-2)Rw(k)+w^T(k)Rw(k)w(k)]
    +0.5[1-w^T(k)w(k)]w(k).
```

于是有

$$\left.\frac{\partial G}{\partial w}\right|_{0}=I+2\eta C-\eta w^{T}(k)w(k)C-\eta w^{T}(k)Cw(k)I-4\eta Cw(k)w^{T}(k), \tag{5.29}$$

其中

$$C=\frac{1}{4\eta}I-R,$$

`I`为单位矩阵。对于平衡点`0`，由(5.29)可得

$$\left.\frac{\partial G}{\partial w}\right|_{0}=I+2\eta C=1.5I-2\eta R=J_0.$$

记`J_0`的第`i`个特征值为`α_0^{(i)}`。由`ηλ_1<0.25`，有

$$\alpha_0^{(i)}=1.5-2\eta\lambda_i\ge 1.5-2\eta\lambda_1>1,\quad (i=1,2,\ldots,n).$$

根据李雅普诺夫理论，平衡点`0`是不稳定的。

对于平衡点`±v_j` (`j=1,…,n`)，由(5.29)可得

$$\left.\frac{\partial G}{\partial w}\right|_{v_j}=(1+\eta\lambda_j)I-\eta R-(1-4\eta\lambda_j)v_jv_j^T=J_j.$$

记`J_j`的第`i`个特征值为`α_j^{(i)}`。显然，

$$\alpha_j^{(i)}=1+\eta(\lambda_j-\lambda_i)\quad\text{if }i\ne j.$$

$$\alpha_j^{(j)}=4\eta\lambda_j\quad\text{if }i=j.$$

对任意`j≠n`，有

$$\alpha_j^{(n)}=1+\eta(\lambda_j-\lambda_n)>1.$$

显然，平衡点`±v_j` (`j≠n`)是不稳定的。对于平衡点`±v_n`，由于`ηλ_1<0.25`，可得

$$\alpha_n^{(i)}=1+\eta(\lambda_n-\lambda_i)<1\ \text{if }i\ne n.$$

$$\alpha_n^{(i)}=4\eta\lambda_n<4\eta\lambda_1<1\ \text{if }i=n.$$

因此，`±v_n`是渐近稳定的。证毕。

在本节中，我们分析了与所提出的稳定MCA学习算法(5.3)相关联的DDT系统(5.4)的动力学，并证明了(5.4)的权向量在某些条件下将收敛到稳定平衡点`±v_n`。

## 5.4 仿真结果

在本节中，我们提供两个有趣的仿真结果，分别说明所提出的 MCA 算法 (5.3) 在确定性情形和随机情形下的收敛性与稳定性。在这些仿真中，我们将所提出的 MCA 算法 (5.3) 与以下 MCA 算法的性能进行比较：

- **1. Möller MCA 算法** [130]

$$
w(k+1)=w(k)-\eta\left[2w^{T}(k)w(k)-1\right]y(k)x(k)+\eta y^{2}(k)w(k), \tag{5.30}
$$

- **2. Douglas MCA 算法** [60]

$$
w(k+1)=w(k)-\eta w^{T}(k)w(k)w^{T}(k)w(k)y(k)y(k)x(k)+\eta y^{2}(k)w(k), \tag{5.31}
$$

- **3. OJAμ MCA 算法** [68]

$$
w(k+1)=w(k)-\eta y(k)x(k)+\frac{\eta y^{2}(k)w(k)}{w^{T}(k)w(k)w^{T}(k)w(k)}. \tag{5.32}
$$

为了衡量这些算法的收敛速度和精度，我们按照 [31] 计算 `w(k)` 的范数以及 `w(k)` 在更新时的方向：

$$
\mathrm{Direction\ Cosine}(k)=\frac{|w^{T}(k)\cdot v_n|}{\|w(k)\|\cdot\|v_n\|},
$$

其中 `v_n` 是与协方差矩阵 `R` 的最小特征值相关联的特征向量。显然，如果 `Direction Cosine(k)` 收敛到 1，则权重向量 `w(k)` 必定趋向于次分量 `v_n` 的方向。

首先，让我们考虑确定性情形下的性能比较。通过取条件期望，与上述三个 MCA 算法 (5.30)–(5.32) 相对应的 DDT 系统如下：

- **1.** 与 Möller MCA 算法 (5.30) 相关的 DDT 系统：

$$
w(k+1)=w(k)-\eta\left[2w^{T}(k)w(k)-1\right]Cw(k)+\eta w^{T}(k)Cw(k)w(k), \tag{5.33}
$$

- **2.** 与 Douglas MCA 算法 (5.31) 相关的 DDT 系统：

$$
w(k+1)=w(k)-\eta w^{T}(k)w(k)w^{T}(k)w(k)Cw(k)+\eta w^{T}(k)Cw(k)w(k), \tag{5.34}
$$

- **3.** 与 OJAμ MCA 算法 (5.32) 相关的 DDT 系统：

$$
w(k+1)=w(k)-\eta Cw(k)+\frac{\eta w^{T}(k)Cw(k)Cw(k)w(k)}{w^{T}(k)w(k)w^{T}(k)w(k)}. \tag{5.35}
$$

我们随机生成一个 `4×4` 对称正定矩阵：

$$
C^{*}=
\begin{bmatrix}
1.6064 & 0.2345 & 0.6882 & 1.2175 \\
0.2345 & 1.6153 & 0.3753 & 0.0398 \\
0.6882 & 0.3753 & 1.8981 & 0.6181 \\
1.2175 & 0.0398 & 0.6181 & 1.1799
\end{bmatrix}
$$

![](img/5d1bf22d32ba379cbf31221a5347fdb6_141_0.png)

**图 5.1** 确定性情形下 `‖w(k)‖` 的收敛性。
