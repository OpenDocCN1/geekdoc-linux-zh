
`w(k+1)=w(k)+\eta[-\sigma g(w(k))-f(\lVert w(k)\rVert^2)w(k)]`.

\]
对于所有 \(k\ge 0\)，其中 \(f\) 是标量函数，\(\eta>0\) 是固定学习率。显然，若 \(\sigma=1\)，算法可重写为：

```
w(k+1)=w(k)+\eta[-(aw(k)-bw^3(k))-f(\lVert w(k)\rVert^2)w(k)]. \tag{7.1}
```

若 \(\sigma=-1\)，则有：

```
w(k+1)=w(k)+\eta[(aw(k)-bw^3(k))-f(\lVert w(k)\rVert^2)w(k)]. \tag{7.2}
```

本章将说明算法(7.1)和(7.2)在某些条件下既具有稳定性又具有混沌行为。将推导这些稳定与混沌的条件。因此，容易看出，通过选择合适的学习参数可以避免发散行为和混沌行为。

本章组织如下。第2节确定了一些不变集，并得到这些算法发散的条件。第3节推导了这些算法的稳定性条件。第4节分析了混沌及混沌行为。最后，第5节给出结论。

### 7.2 不变集与发散

显然，不变集保证算法的不发散性。下面的定理将给出算法(7.1)和(7.2)的不变集。为了便于分析，首先给出两个引理。

记

```
M_1^*=\max\left\{\frac{a+f(\lVert w(k)\rVert^2)}{b},\frac{4\left(\eta(a+f(\lVert w(k)\rVert^2))-1\right)^3}{27\eta b}\right\},
```

```
M_2^*=\max\left\{\frac{\eta(a-f(\lVert w(k)\rVert^2))+2}{\eta b},\frac{4\left(\eta(a-f(\lVert w(k)\rVert^2))+1\right)^3}{27\eta b}\right\}.
```

**引理 7.1** 假设 `\eta>0`、`a>0`、`b>0`。则有

```
[1-\eta a-\eta f(\lVert w(k)\rVert^2)+\eta bs]\cdot s\le M_1^*,
```

对于所有 `0<s\le\dfrac{a+f(\lVert w(k)\rVert^2)}{b}` 且 `\eta(a+f(\lVert w(k)\rVert^2))>0` 成立。

**证明：** 定义一个可微函数

```
f(s)=\left[1-\eta a-\eta f(\|w(k)\|^2)+\eta bs\right]^2\cdot s,
```

对于所有 `0<s\leq \dfrac{a+f(\|w(k)\|^2)}{b}`。则有

```
\dot f(s)=\left[1-\eta a-\eta f(\|w(k)\|^2)+\eta bs\right]\left[1-\eta a-\eta f(\|w(k)\|^2)+3\eta bs\right],
```

对于所有 `0<s\leq \dfrac{a+f(\|w(k)\|^2)}{b}`。记

```
\xi_1=\dfrac{\eta(a+f(\|w(k)\|^2))-1}{3\eta b},\qquad \xi_2=\dfrac{\eta(a+f(\|w(k)\|^2))-1}{\eta b}.
```

若 `\eta(a+f(\|w(k)\|^2))>1`，则有

```
\dot f(s)\begin{cases}
>0, & \text{若 }0<s<\xi_1,\\
=0, & \text{若 }s=\xi_1,\\
<0, & \text{若 }\xi_1<s<\xi_2,\\
=0, & \text{若 }s=\xi_2,\\
>0, & \text{若 }s>\xi_2.
\end{cases}
```

这表明函数 `f(s)` 在区间 `\left(0,\dfrac{a+f(\|w(k)\|^2)}{b}\right)` 上的最大值点必为 `s^*=\xi_1` 或 `s^*=\dfrac{a+f(\|w(k)\|^2)}{b}`。若 `\eta(a+f(\|w(k)\|^2))\leq 1`，则 `s^*=\dfrac{a+f(\|w(k)\|^2)}{b}` 必为 `f(s)` 在区间 `\left(0,\dfrac{a+f(\|w(k)\|^2)}{b}\right)` 上的最大值点。因此，不难得到

```
\left[1-\eta a-\eta f(\|w(k)\|^2)+\eta bs\right]^2\cdot s\leq M_1^*,
```

对于所有 `0<s\leq \dfrac{a+f(\|w(k)\|^2)}{b}`。证毕。

#### 引理 7.2

假设 `\eta>0`，`a>0`，且 `b>0`。则有

```
\left[1+\eta a-\eta f(\|w(k)\|^2)-\eta bs\right]^2\cdot s\leq M_2^*,
```

对于所有 `0<s\leq \dfrac{\eta(a-f(\|w(k)\|^2))+2}{\eta b}`，其中 `\eta(a-f(\|w(k)\|^2))>-2`。

**证明：** 定义一个可微函数

```
f(s)=\left[1+\eta a-\eta f(\|w(k)\|^2)-\eta bs\right]^2\cdot s
```

对于所有 `0<s\leq \dfrac{\eta(a-f(\|w(k)\|^2))+2}{\eta b}`。则有

```
\dot f(s)=\left[1+\eta a-\eta f(\|w(k)\|^2)-\eta bs\right]\left[1+\eta a-\eta f(\|w(k)\|^2)-3\eta bs\right],
```

对于所有 `0<s\leq \dfrac{\eta(a-f(\|w(k)\|^2))+2}{\eta b}`。记

```
\xi_1=\dfrac{\eta(a-f(\|w(k)\|^2))+1}{3\eta b},\qquad \xi_2=\dfrac{\eta(a-f(\|w(k)\|^2))+1}{\eta b}.
```

若 `\eta(a-f(\|w(k)\|^2))>-1`，则有

```
\dot f(s)\begin{cases}
>0, & \text{若 }0<s<\xi_1,\\
=0, & \text{若 }s=\xi_1,\\
<0, & \text{若 }\xi_1<s<\xi_2,\\
=0, & \text{若 }s=\xi_2,\\
>0, & \text{若 }s>\xi_2.
\end{cases}
```

这表明函数 `f(s)` 在区间 `\left(0,\dfrac{\eta(a-f(\|w(k)\|^2))+2}{\eta b}\right)` 上的最大值点必为 `s^*=\xi_1` 或 `s^*=\dfrac{\eta(a-f(\|w(k)\|^2))+2}{\eta b}`。

若 `-2<\eta(a-f(\|w(k)\|^2))\leq -1`，`s^*=\dfrac{\eta(a-f(\|w(k)\|^2))+2}{\eta b}` 必为 `f(s)` 的最大值点。因此，不难得到

```
\left[1+\eta a-\eta f(\|w(k)\|^2)-\eta bs\right]^2s\leq M_2^*,
```

对于所有 `0<s\leq \dfrac{\eta(a-f(\|w(k)\|^2))+2}{\eta b}`。证毕。

#### 引理 7.3

若 `0<x\leq 4`，则成立 `(x-1)^3\leq \dfrac{27x}{4}`。

**证明：** 定义一个可微函数

```
f(x)=(x-1)^3-\frac{27x}{4},
```

对于所有 `0<x\leq 4`。则有

```
\dot f(x)=3(x-1)^2-\frac{27}{4},
```

记

```
S_1=\left\{w^2\mid w^2\in\mathbb{R},\ w^2<\frac{a+f(\|w(k)\|^2)}{b}\right\},
```

```
S_2=\left\{w^2\mid w^2\in\mathbb{R},\ w^2<\frac{a-f(\|w(k)\|^2)}{b}+\frac{2}{\eta b}\right\}.
```

#### 定理 7.1

假设 `\eta>0`，`a>0`，且 `b>0`。若 `0<\eta(a+f(\|w(k)\|^2))\leq 4`，则 `S_1` 是 (7.1) 的不变集。若 `-2<\eta(a-f(\|w(k)\|^2))\leq 2`，则 `S_2` 是 (7.2) 的不变集。

**证明：** 由 (7.1) 可得
