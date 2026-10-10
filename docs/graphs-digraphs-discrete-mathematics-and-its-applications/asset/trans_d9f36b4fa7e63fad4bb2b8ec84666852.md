

## 第 16.5 节

- 11. 回想一下，图 *G*（阶数为 *n*）的色多项式可以表示为
  $$P(G, \lambda) = \lambda^n - a_1 \lambda^{n-1} + a_2 \lambda^{n-2} + \dots + (-1)^{n+1} a_{n-1} \lambda .$$

- 13. (a) 参见下图。

![](img/598a6ae3fd44120830ada34717906f29_596_0.png)

(b) $P(K_{2,2,2}, 3) = 6 = \chi(K_{2,2,2})!$

- 15. (a) 两个阶数相同且包含相同长度环的单环图在色度上是等价的。

(b) *n* - 2。

- 17. (a) 假设该陈述为假。那么在所有反例中，设 *S* 为阶数 *n* 最小的那些反例的集合，设 *G* 为 *S* 中大小 *m* 最小的图。则 $P(G, \lambda) = \lambda g(\lambda)$，其中 $g(0) = 0$。因此 *G* 不是一棵树。设 $e = uv$ 是 *G* 中不是桥的一条边，设 *H* 为在 $G - e$ 中合并 *u* 和 *v* 后得到的图。考虑 $P(G, \lambda)$，$P(G - e, \lambda)$ 和 $P(H, \lambda)$ 中 $\lambda$ 的系数。

(b) 应用练习题 16 和 (a)。

- 19. 对 *G* 中连通分支（块）的数量进行归纳，并应用练习题 16。

- 21. 由于 $K_{r,r}$ 是唯一一个阶数为 2*r* 且大小为 $r^2$ 的二分图，因此它是色度唯一的。

- 23. 图 *G* 的顶点可以列举为 $v_1, v_2, \dots, v_n$，使得 $v_i$（$2 \leq i \leq n$）与 $\{v_1, v_2, \dots, v_{i-1}\}$ 中至少一个顶点相邻。考虑使用此顺序对 *G* 的顶点进行着色的方式数量。

- 25. 该陈述是正确的。

## 第 16.6 节

- 27. (a) 参见下图。(b) 根据广义欧拉恒等式（定理 11.10），$r = 5$。(c) 需要五种颜色。

![](img/598a6ae3fd44120830ada34717906f29_597_0.png)

- 29. 考虑图 $K_8$。

## 第 17 章

### 第 17.1 节

- 1. 该图的色边指数为 4。
- 3. 由于 $\Delta(G \square K_2) = 1 + \Delta(G)$，只需证明存在 $G \square K_2$ 的 $(1 + \Delta(G))$-边着色。因为 $\chi'(G) \leq 1 + \Delta(G)$，所以存在 $G$ 的 $(1 + \Delta(G))$-边着色。
- 5. (a) 观察到 $G$ 包含子图 $G_1$、$G_2$ 和完全二分图 $K_{n_1,n_2}$。
(b) 考虑 $G_1 = K_2$ 和 $G_2 = C_5$。

### 第 17.2 节

- 7. 证明 $G$ 是过剩的，并应用推论 17.9。
- 9. 由于 $G$ 是 3-正则的，因此 $G$ 具有偶数阶。考虑 $G$ 的哈密顿环 $C$。
- 11. 每个正多面体的图都是 I 类的。
- 13. 证明存在一个 $\Delta(G)$-正则二分图，其中包含 $G$ 作为诱导子图。
- 15. 应用定理 17.8。
- 17. 设 $G = C_n \square K_2$，其中 $n \geq 3$ 为奇数。
- 19. 应用定理 17.8。
- 21. 应用推论 17.9。
- 23. (a) 法国队有连续两天休息。
(b) 选手 B 只在第 4 天参加一场比赛，而其他选手每天至少参加两场比赛。
- 25. 图 $G$ 是过剩的。

### 第 17.3 节

- 27. (a) 否。(b) 是。
- 29. (a) 否。(b) 否。(c) 是。
- 31. (a) $\chi'(G) = 4$。(b) 否。

## 第 18 章

### 第 18.1 节

- 1. 参见下图。

![](img/598a6ae3fd44120830ada34717906f29_598_0.png)

- 3. 证明对于整数 $a$ 和 $b$ 以及 $D$ 的每个顶点 $v$，$\sigma^+(v; a\omega_1 + b\omega_2) = \sigma^-(v; a\omega_1 + b\omega_2)$。

- 5. 设 $G$ 为一个无桥图，包含一条欧拉径，设 $u$ 和 $v$ 为 $G$ 的两个奇度顶点。则 $G$ 是 2-边连通的，根据定理 4.18，$G$ 包含两条边不交（边互不相交）的 $u-v$ 路径 $P$ 和 $P'$。通过为这些路径中适当定向的边分配流值开始。

- 7. 设 $V(K_6) = \{1, 2, 3, 4, 5, 6\}$。$K_6$ 的一个由五个哈密顿环组成的圈双覆盖为 $(1,2,3,4,5,6,1)$，$(1,3,6,2,5,4,1)$，$(1,4,2,6,5,3,1)$，$(1,5,2,3,4,6,1)$，$(1,2,4,6,5,3,1)$。

### 第 18.2 节

- 9. 设 $\Delta(G) = \Delta$，对于 $G$ 的每条边 $e$，设 $L(e)$ 为 $2\Delta - 1$ 种颜色（正整数）的列表。设 $e_1, e_2, \dots, e_m$ 为 $G$ 边的一个排序，并对边进行贪心着色。

### 第 18.3 节

- 11. $\chi(G) = 3$，$\chi'(G) = 4$ 且 $\chi''(G) = 5$。
- 13. $\chi'(G) = 4$。
- 15. 由于 $\Delta(K_{s,t}) = t$，因此 $\chi''(K_{s,t}) \geq t + 1$。描述 $K_{s,t}$ 的一个 $(t + 1)$-总着色。

## 第 19 章

### 第 19.1 节

- 1. $T_{7,2} = K_{3,4}$，$t_{7,2} = 12$，$T_{7,3} = K_{2,2,3}$，$t_{7,3} = 16$，$T_{7,4} = K_{1,2,2,2}$，$t_{7,4} = 18$，$T_{8,2} = K_{4,4}$，$t_{8,2} = 16$，$T_{8,3} = K_{2,2,3}$，$t_{8,3} = 21$，$T_{8,4} = K_{2,2,2,2}$，$t_{8,4} = 24$。
- 3. $m = 13$。
- 5. 证明 $G$ 包含一个度数为 2 或更高的顶点。
- 7. 对于 $n \geq 4$，最小的整数 $m$，使得每个阶数为 $n$ 且大小为 $m$ 的图都包含 $\overline{K}_{1,3}$ 作为子图，是 $n + 1$。
- 9. (a) 设 $e = uv$ 为 $G$ 的一条边，设 $A = N(u) - \{v\}$ 且 $B = N(v) - \{u\}$。首先证明 $|A \cap B| \geq \lceil n + 2 \rceil/3$。
(b) 对于整数 $r \geq 3$，设 $G = K_{r,r,r}$。
- 11. $m = \lceil n^2/4 \rceil + 2$。

### 第 19.2 节

- 13. 设 $g=g(G)$。考虑 $g$ 为偶数或 $g$ 为奇数的情况。
- 15. 假设 $H$ 是一个 $(s,g)$-图，并反过来假设 $H$ 是一个 $(s,g)$-笼。由于 $H$ 包含 4-环，因此要么 $g=3$ 要么 $g=4$。
- 17. (a) $n(4,3,4)=5$。(b) $n(4,3,6)=8$。

## 第 20 章

### 第 20.1 节

- 1. (a) 考虑 $H=G \vee K_1$。(b) 考虑 $F = G + K_1$。
- 3. 为了证明 $R(s,t') \le R(s,t)$，设 $G$ 为阶数为 $R(s,t)$ 的图。然后应用拉姆齐数的定义。
- 5. 为了证明 $R(4,4) \le 18$，考虑 $K_{18}$ 的红蓝着色。$K_{18}$ 的每个顶点与九条同颜色的边相连。
- 7. $\min \{t_i \} = 2$。
- 9. 否。

### 第 20.2 节

- 11. $R(F,H)=7$。
- 13. $R(K_3,C_5)=9$。
- 15. 考虑 $n$ 为偶数和 $n$ 为奇数的情况。应用定理 13.5 和 13.2。
- 17. (a) 是。(b) 设 $n=R_\chi(s-1,t)+R_\chi(s,t-1)$。给定完全图 $K_n$ 的一个红蓝着色。证明 $K_n$ 包含一个色数至少为 $s$ 的红色子图，或包含一个色数至少为 $t$ 的蓝色子图。
(c) $R_\chi(3,3)=5$。(d) 对于 $3 \le s \le t$，$R_\chi(s,t) = 1 + (s-1)(t-1)$。
- 19. 设 $n=R(K_{n_1},K_{n_2}, \dots, K_{n_r}, T_n)$。为了证明 $n \le 1 + (r-1)(s-1)$，应用定理 12.21。为了证明 $n \ge 1+(r-1)(s-1)$，展示 $K_{(r-1)(s-1)}$ 的一个边着色，使用颜色 $1,2, \dots,k+1$，使得对于每个满足 $1 \le i \le k$ 的 $i$，不存在一个所有边都染为颜色 $i$ 的 $K_{n_i}$ 副本，也不存在一个所有边都染为颜色 $k+1$ 的 $T_n$ 副本。
- 21. (a) $R(K_1,3,K_3)=7$。(b) $MR(K_{1,3},K_3)=6$。
- 23. $MR(F,H)=6$。
- 25. $RR(K_{1,3},P_4)=5$。
- 27. $BR(P_4,P_4)=3$。

## 第 21 章

### 第 21.1 节

- 1. 遵循定理 21.1 的证明。
- 3. 确定 $\log_2 10$ 的上界。
- 5. 考虑概率空间 $S$，其元素是 $\binom{n}{2}$ 个不同的有标签竞赛图 $T$，顶点集为 $V(T)=\{v_1,v_2,\dots,v_n\}$。概率由以下定义：对于 $T$ 中每对不同顶点 $v_i,v_j$，$P((v_i,v_j) \in E(T)) = P((v_j,v_i) \in E(T)) = \frac{1}{2}$，并且这些事件是相互独立的。对于每个 $k$ 元子集 $U \subseteq \{v_1, v_2, \dots, v_n\}$，考虑事件“$V(G)-U$ 中没有顶点与 $U$ 中的每个顶点都相邻”的概率。

### 第 21.2 节

- 7. 将定理 21.7 应用于性质 $Q_{2.0}$。
- 9. 设 $n$ 为一个正整数，使得 $(n-3)(n-4)/12 > k$。根据定理 21.9，几乎所有的图都包含 $K_n$ 作为子图。根据定理 11.18，$\gamma(K_n) > k$。因此，几乎所有的图的亏格都超过 $k$，从而几乎没有图的亏格小于或等于 $k$。
- 11. 证明如果 $r(n)$ 是某个性质的阈值函数，那么 $2r(n)$ 也是。对于任意常数 $c > 0$，$cr(n)$ 呢？
- 13. 考虑直径为 2 的连通图的偏心率序列。

# 参考文献

- [1] B. M. Ábreço, S. Fernández-Merchant and G. Salazar, The rectilinear crossing number of $K_n$: Closing in (or are we?) *Thirty essays on geometric graph theory* 5-18, Springer, New York, 2013. [286]
- [2] Y. Alavi, A. J. Boals, G. Chartrand, P. Erdős and O. R. Oellermann, The ascending subgraph decomposition problem. *Congr. Numer.* **58** (1987) 7-14. [345]
- [3] N. Alon, Choice numbers of graphs; a probabilistic approach, *Comb. Prop. Comput.* **1** (1992) 107-114. [409]
- [4] B. Alspach, Research problems, Problem 3. *Discrete Math.* **36** (1981) 333. [349]
- [5] B. Alspach, The wonderful Walecki construction. *Bull. Inst. Combin. Appl.* **52** (2008) 7-20. [341]
- [6] B. Alspach and H. Gavlas, Cycle decompositions of $K_n$ and $K_n-I$. *J. Combin. Theory Ser B* **81** (2001) 77-99. [348, 350]
- [7] V. I. Arnautov, Estimation of the exterior stability number of a graph by means of the minimal degree of the vertices. (Russian) *Prik. Mat. i Programmivanie Vyp.* **11** (1974) 3-8. [325, 550]
- [8] I. Anderson, Perfect matchings of a graph. *J. Combin. Theory Ser. B* **10** (1971) 183-186. [311]
- [9] K. Appel and W. Haken, Every planar map is four colorable. *Bull. Amer. Math. Soc.* **82** (1976) 711-712. [427]
- [10] D. Archdeacon and P. Huneke, A Kuratowski theorem for nonorientable surfaces. *J. Combin. Theory Ser. B* **46** (1989) 173-231. [300]
- [11] A. T. Balaban, Trivalent graphs of girth nine and eleven, and relationships among cages. *Rev. Roumaine Math. Pures Appl.* **18** (1973) 1033-1043. [516]

