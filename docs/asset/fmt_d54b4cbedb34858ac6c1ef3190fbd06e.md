
`w^2(k+1)=\left[1-\eta a-\eta f(\|w(k)\|^2)+\eta b w^2(k)\right]^2\cdot w^2(k),`

$$
$$
对于所有 \(k\geq 0\)。因此有
$$
$$
\begin{aligned}
w^2(k+1)&\leq \max\left\{\left[1-\eta a-\eta f(\|w(k)\|^2)+\eta b w^2(k)\right]^2\cdot w^2(k)\right\}\\\
&\leq \max\left\{\left[1-\eta a-\eta f(\|w(k)\|^2)+\eta b s\right]^2\cdot s\right\}.
\end{aligned}
$$
$$
对于所有 \(0<s\leq\dfrac{a+f(\|w(k)\|^2)}{b}\)。由引理 7.1，可得 `w^2(k+1)\leq M_1^*`，其中 `k\geq 0`。由引理 7.3，若 `0<\eta(a+f(\|w(k)\|^2))\leq 4`，则成立
$$
$$
\frac{4(\eta(a+f(\|w(k)\|^2))-1)^3}{27\eta b}\leq\frac{a+f(\|w(k)\|^2)}{b}.
$$
$$
因此可得
$$
$$
w^2(k+1)\leq\frac{a+f(\|w(k)\|^2)}{b}.
$$
$$
因此，`S_1` 是 `(7.1)` 的不变集。

由 `(7.2)` 可得
$$
$$
w^2(k+1)=\left[1+\eta a-\eta f(\|w(k)\|^2)-\eta b w^2(k)\right]^2\cdot w^2(k),
$$
$$
对于所有 `k\geq 0`。因此有
$$
$$
\begin{aligned}
w^2(k+1)&\leq \max\left\{\left[1+\eta a-\eta f(\|w(k)\|^2)-\eta b w^2(k)\right]^2\cdot w^2(k)\right\}\\\
&\leq \max\left\{\left[1+\eta a-\eta f(\|w(k)\|^2)-\eta b s\right]^2\cdot s\right\}.
\end{aligned}
$$
$$
对于所有 `0<s\leq\dfrac{\eta(a-f(\|w(k)\|^2))+2}{\eta b}`。由引理 7.2，可得 `w^2(k+1)\leq M_2^*`，其中 `k\geq 0`。由引理 7.3，若 `-2<\eta(a-f(\|w(k)\|^2))\leq 2`，则成立
$$
$$
\frac{4(\eta(a-f(\|w(k)\|^2))+1)^3}{27\eta b}\leq\frac{\eta(a-f(\|w(k)\|^2))+2}{\eta b}.
$$
$$
因此可得
$$
$$
w^2(k+1)\leq\frac{\eta(a-f(\|w(k)\|^2))+2}{\eta b}.
$$
$$
因此，`S_2` 是 `(7.2)` 的不变集。证毕。

前面的定理表明，从不变集 `S_1` 或 `S_2` 中的 `w(0)` 出发的算法 `(7.1)` 或 `(7.2)` 的任意轨迹都将保持在 `S_1` 或 `S_2` 中。这保证了算法 `(7.1)` 和 `(7.2)` 的不发散性。然而，在不变集之外，算法表现出不同的动力学行为，甚至可能发散到无穷大。以下定理给出算法的发散条件。

#### 定理 7.2
假设 `η>0`，`a>0`，`b>0`，且 `w(0)\neq 0`。

对于算法 `(7.1)`，若 `0<\eta(a+f(\|w(k)\|^2))` 且
$$
$$
w^2(k)>\frac{a+f(\|w(k)\|^2)}{b},
$$
$$
则
$$
$$
\lim_{k\to+\infty}w^2(k+1)=+\infty.
$$
$$
对于算法 `(7.2)`，若 `-2<\eta(a-f(\|w(k)\|^2))` 且
$$
$$
w^2(k)>\frac{\eta(a-f(\|w(k)\|^2))+2}{\eta b},
$$
$$
则
$$
$$
\lim_{k\to+\infty}w^2(k+1)=+\infty.
$$
$$
**证明：** 由 `(7.1)` 可得
$$
$$
w^2(k+1)=\left[1-\eta a-\eta f(\|w(k)\|^2)+\eta b w^2(k)\right]^2\cdot w^2(k),
$$
$$
对于所有 `k\geq 0`。若
$$
$$
w^2(k)>\frac{a+f(\|w(k)\|^2)}{b},
$$
$$
对于所有 `k\geq 0` 成立，则有
$$
$$
1-\eta a-\eta f(\|w(k)\|^2)+\eta b w^2(k)>1,
$$
$$
对于所有 `k\geq 0` 成立。于是有
$$
$$
\left[1-\eta a-\eta f(\|w(k)\|^2)+\eta b w^2(k)\right]^2>1,
$$
$$
对于所有 `k\geq 0` 成立。因此，对于算法 `(7.1)`，有
$$
$$
\lim_{k\to+\infty}w^2(k+1)=+\infty.
$$
$$
由算法 `(7.2)` 可得
$$
$$
w^2(k+1)=\left[1+\eta a-\eta f(\|w(k)\|^2)-\eta b w^2(k)\right]^2\cdot w^2(k),
$$
$$
对于所有 `k \ge 0`。若
$$
$$
w^2(k)>\frac{\eta\left(a-f(\|w(k)\|^2)\right)+2}{\eta b},
$$
$$
对于所有 `k \ge 0` 成立，则有
$$
$$
1+\eta a-\eta f(\|w(k)\|^2)-\eta b w^2(k)<-1,
$$
$$
对于所有 `k \ge 0` 成立。容易看出
$$
$$
\left[1+\eta a-\eta f(\|w(k)\|^2)-\eta b w^2(k)\right]^2>1,
$$
$$
对于所有 `k \ge 0` 成立。因此，对于算法 `(7.2)`，\(\displaystyle\lim_{k\to+\infty}w^2(k+1)=+\infty\)。

证毕。

#### 定理 7.3
假设 `η>0`，`a>0`，`b>0`，且 `w(0)\ne 0`。对于算法 `(7.1)`，若 `η(a+f(\|w(k)\|^2))\le 0`，则 \(\displaystyle\lim_{k\to+\infty}w^2(k+1)=+\infty\)。对于算法 `(7.2)`，若 `η(a-f(\|w(k)\|^2))\le -2`，则 \(\displaystyle\lim_{k\to+\infty}w^2(k+1)=+\infty\)。

**证明：** 由 `(7.1)` 可得
$$
$$
w^2(k+1)=\left[1-\eta a-\eta f(\|w(k)\|^2)+\eta b w^2(k)\right]^2\cdot w^2(k),
$$
$$
对于所有 `k\ge 0`。若 `η(a+f(\|w(k)\|^2))\le 0` 且 `w(0)\ne 0`，则对于所有 `k\ge 0` 有
$$
$$
\left[1-\eta a-\eta f(\|w(k)\|^2)+\eta b w^2(k)\right]^2>1,
$$
$$
因此，对于算法 `(7.1)`，有 \(\displaystyle\lim_{k\to+\infty}w^2(k+1)=+\infty\)。

由算法 `(7.2)` 可得
$$
$$
w^2(k+1)=\left[1+\eta a-\eta f(\|w(k)\|^2)-\eta b w^2(k)\right]^2\cdot w^2(k),
$$
$$
对于所有 `k\ge 0`。若 `η(a-f(\|w(k)\|^2))\le -2` 且 `w(0)\ne 0`，则对于所有 `k\ge 0` 有
$$
$$
\left[1+\eta a-\eta f(\|w(k)\|^2)-\eta b w^2(k)\right]^2>1,
$$
$$
因此，对于算法 `(7.2)`，\(\displaystyle\lim_{k\to+\infty}w^2(k+1)=+\infty\)。

证毕。

由前面的定理，不变集和发散区域如图 7.1 和图 7.2 所示。`S_1` 和 `S_2` 分别是算法 `(7.1)` 和 `(7.2)` 的不变集。区域 `I`、`II` 和 `III` 是发散区域。在区域 `IV` 中，算法的有界性无法得到保证。下面的例子（图 7.3）说明了 `(7.1)` 和 `(7.2)` 在区域 `IV` 中的发散性。

![](img/5d1bf22d32ba379cbf31221a5347fdb6_182_0.png)

**图 7.1**

算法（7.1）的不变集 `S_1`，以及发散区域 `I`、`II` 和 `III`。
