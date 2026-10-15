
## 定理 11.4
若 $s$ 和 $t$ 是满足 $s \leq t$ 的正整数，且要么 (1) $s \leq 6$ 要么 (2) $s = 7$ 且 $t \leq 10$，则

$$ \operatorname{cr}(K_{s,t}) = \left\lfloor \frac{s}{2} \right\rfloor \left\lfloor \frac{s-1}{2} \right\rfloor \left\lfloor \frac{t}{2} \right\rfloor \left\lfloor \frac{t-1}{2} \right\rfloor \text{.} $$

因此，由定理 11.4 可知

$$ \operatorname{cr}(K_{3,t}) = \left\lfloor \frac{t}{2} \right\rfloor \left\lfloor \frac{t-1}{2} \right\rfloor \text{,} \quad \quad \operatorname{cr}(K_{4,t}) = 2 \left\lfloor \frac{t}{2} \right\rfloor \left\lfloor \frac{t-1}{2} \right\rfloor \text{,} $$

$$ \operatorname{cr}(K_{5,t}) = 4 \left\lfloor \frac{t}{2} \right\rfloor \left\lfloor \frac{t-1}{2} \right\rfloor \text{ 且 } \operatorname{cr}(K_{6,t}) = 6 \left\lfloor \frac{t}{2} \right\rfloor \left\lfloor \frac{t-1}{2} \right\rfloor $$

对所有 $t$ 成立。例如，$\operatorname{cr}(K_{3,3}) = 1$，$\operatorname{cr}(K_{4,4}) = 4$，$\operatorname{cr}(K_{5,5}) = 16$，$\operatorname{cr}(K_{6,6}) = 36$ 且 $\operatorname{cr}(K_{7,7}) = 81$。$K_{4,4}$ 具有四个交叉的绘法如附图 11.3 所示。

![](img/598a6ae3fd44120830ada34717906f29_292_0.png)

图 11.3: 具有四个交叉的 $K_{4,4}$ 绘法

不出所料，关于完全 $k$-部图（$k \geq 3$）交叉数的情况甚至更加复杂。在大多数情况下，这些情形中仅获得了界限和高度具体的结果。另一方面，所采用的一些证明技术具有启发意义。作为一个例子，以下亚瑟·T·怀特（Arthur T. White）[254, p. 67] 的结果确立了 $K_{2,2,3}$ 的交叉数。

## 定理 11.5
$K_{2,2,3}$ 的交叉数为 2。

### 证明
图 $K_{2,2,3}$ 的阶为 7，规模为 16。假设 $\mathrm{cr}(K_{2,2,3}) = c$。由于 $K_{3,3}$ 是非平面图且 $K_{3,3} \subseteq K_{2,2,3}$，因此 $K_{2,2,3}$ 是非平面图，故 $c \geq 1$。设给定 $K_{2,2,3}$ 在平面上的一个具有 $c$ 个交叉的绘法。在每个交叉点我们引入一个新顶点，从而生成一个连通平面图 $G$，其阶 $n = 7 + c$，规模 $m = 16 + 2c$。由定理 10.3，$m \leq 3n - 6$。

设 $u_1u_2$ 和 $v_1v_2$ 是 $K_{2,2,3}$ 中两个（不相邻的）在给定绘法中相交的边，产生一个新顶点。如果 $G$ 是一个极大平面图，那么 $C = \langle u_1, v_1, u_2, v_2, u_1 \rangle$ 是 $G$ 的一个圈，这意味着 $\{u_1, u_2, v_1, v_2\}$ 在 $K_{2,2,3}$ 中诱导的子图是 $K_4$。然而，$K_{2,2,3}$ 不包含这样的子图；因此，$G$ 不是一个极大平面图，故 $m < 3n - 6$。因此，

$$ 16 + 2c < 3(7 + c) - 6, $$

由此得出 $c \geq 2$。不等式 $c \leq 2$ 源于存在一个具有两个交叉的 $K_{2,2,3}$ 绘法这一事实（见图 11.4）。

![](img/598a6ae3fd44120830ada34717906f29_292_1.png)

图 11.4: 具有两个交叉的 $K_{2,2,3}$ 绘法

### 图笛卡尔积的交叉数
其他其交叉数已被研究但收效甚微的图是 $n$-超立方体 $Q_n$。由于 $Q_n$ 对于 $n = 1, 2, 3$ 是平面图，因此对于这样的每个 $n$，$\operatorname{cr}(Q_n) = 0$。罗杰·埃格顿（Roger Eggleton）和理查德·盖伊（Richard Guy）[76] 证明了 $\operatorname{cr}(Q_4) = 8$，但对于 $n \geq 5$，$\operatorname{cr}(Q_n)$ 未知。人们可能会注意到

$$ Q_4 = K_2 \square K_2 \square K_2 \square K_2 = C_4 \square C_4 $$

因此 $\operatorname{cr}(C_4 \square C_4) = 8$。这引出了确定 $s, t \geq 3$ 时 $\operatorname{cr}(C_s \square C_t)$ 的问题。对于 $s = t = 3$ 的情形，弗兰克·哈利（Frank Harary）、保罗·凯恩（Paul Kainen）和艾伦·施温克（Allen Schwenk）[120] 证明了 $\operatorname{cr}(C_3 \square C_3) = 3$。他们的证明由以下三个步骤组成：

- 步骤 1. 展示 $C_3 \square C_3$ 的一个具有三个交叉的绘法，从而 $\operatorname{cr}(C_3 \square C_3) \leq 3$。
- 步骤 2. 证明对于 $C_3 \square C_3$ 的每条边 $e$，$C_3 \square C_3 - e$ 都是非平面图，从而 $\operatorname{cr}(C_3 \square C_3) \geq 2$。
- 步骤 3. 通过分情况穷举，证明不可能存在 $C_3 \square C_3$ 具有恰好两个交叉的绘法，从而 $\operatorname{cr}(C_3 \square C_3) \geq 3$（见练习 6）。

理查德·D·林格森（Richard D. Ringeisen）和洛厄尔·W·贝尼基（Lowell W. Beineke）[200] 随后通过确定所有整数 $t \geq 3$ 的 $\operatorname{cr}(C_3 \square C_t)$ 显著扩展了这一结果。

## 定理 11.6
对于每个整数 $t \geq 3$，$\operatorname{cr}(C_3 \square C_t) = t$。

### 证明
我们将 $C_3 \square C_t$ 的顶点标记为 $3t$ 个有序对 $(0,j)$，$(1,j)$ 和 $(2,j)$，其中 $j = 0,1,\dots,t - 1$，为了方便，我们令

$$ u_j = (0,j), \quad v_j = (1,j) \text{ 且 } w_j = (2,j). $$

首先，我们注意到 $\operatorname{cr}(C_3 \square C_t) \leq t$。这一观察源于存在一个具有 $t$ 个交叉的 $C_3 \square C_t$ 绘法这一事实。$C_3 \square C_4$ 具有四个交叉的绘法如附图 11.5 所示。对于其他 $t$ 值，$C_3 \square C_t$ 具有 $t$ 个交叉的绘法可以类似给出。

![](img/598a6ae3fd44120830ada34717906f29_294_0.png)

图 11.5: 具有四个交叉的 $C_3 \square C_4$ 绘法

情形 1. 任意三角形 $T_j = G[\{u_j, v_j, w_j\}]$，$j = 0, 1, \dots, k$ 的边都没有被交叉。 对于 $j = 0, 1, \dots, k$，定义

$$ H_j = G[\{u_j, w_j, w_{j+1}, u_{j+1}, v_{j+1}, w_{j+1}\}], $$
