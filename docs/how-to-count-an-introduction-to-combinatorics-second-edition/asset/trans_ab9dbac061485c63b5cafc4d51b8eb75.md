

因此，在 1 到 1,000,000 的范围内，不被 2、3、5 和 7 中任何数整除的整数个数为 1,000,000 - 771,429 = 228,571。

### 4.1.3A

令 $V_1$、$V_2$、$V_3$ 和 $V_4$ 分别为没有黑桃、红心、方块和梅花的大桥牌手牌集合。我们寻求 $\#(V_1 \cup V_2 \cup V_3 \cup V_4)$ 的值。根据容斥原理，该值等于

$$
\sum_{1\le i\le4}\#(V_i)-\sum_{1\le i< j \le4}\#(V_i\cap V_j)+\sum_{1\le i<j< k\le4}\#(V_i\cap V_j\cap V_k)-\#(V_1\cap V_2\cap V_3\cap V_4). \tag{1}
$$

对于 $1 \le i \le 4$，$V_i$ 中的手牌由从未被排除的三花色中的 39 张牌中抽取的 13 张组成。因此 $\#(V_i)=\mathrm{C}(39,13)$。对于 $1 \le i < j \le 4$，$V_i \cap V_j$ 中的手牌由从未被排除的两花色中的 26 张牌中抽取的 13 张组成。因此，$\#(V_i \cap V_j) =\mathrm{C}(26,13)$。类似地，对于 $1 \le i < j < k \le 4$，$\#(V_i \cap V_j \cap V_k)=\mathrm{C}(13,13)$。不存在四个花色均无牌的大桥牌手牌，因此 $\#(V_1 \cap V_2 \cap V_3 \cap V_4)=0$。因此，根据公式 1，

$$
\#(V_1 \cup V_2 \cup V_3 \cup V_4)=4 \times \mathrm{C}(39,13)-6 \times \mathrm{C}(26,13)+4 \times \mathrm{C}(13,13)-0=32,427,298,180.
$$

### 4.1.4A

一个小于或等于 $n$ 的正整数与 $n$ 有公因数当且仅当它能被 $p_1, p_2, \ldots, p_k$ 中的一个整除。令 $E_i$（其中 $1 \le i \le k$）为 1 到 $n$ 范围内能被 $p_i$ 整除的整数集合。因此 $\#\left(\phi(n)\right)=n-\#\left(\cup_{i=1}^k E_i\right)$。根据容斥原理，

$$
\#\left(\bigcup_{i=1}^k E_i\right)=\sum_{1 \le i \le k} \#(E_i)-\sum_{1 \le i < j \le k} \#(E_i \cap E_j)+... =\sum_{1 \le i \le k} \frac{n}{p_i}-\sum_{1 \le i < j \le k} \frac{n}{p_i p_j}+...
$$

从而可得

$$
\phi(n)=n-\sum_{1 \le i \le k} \frac{n}{p_i}+\sum_{1 \le i < j \le k} \frac{n}{p_i p_j}-...=n\left(1-\sum_{1 \le i \le k} \frac{1}{p_i}+\sum_{1 \le i < j \le k} \frac{1}{p_i p_j}-...\right).
$$

因此，利用代数恒等式 $(1-x_1)(1-x_2)...(1-x_k)=1-\sum_{1 \le i \le k} x_i+\sum_{1 \le i < j \le k} x_ix_j-...$，可得

$$
\phi(n)=n\left(1-\frac{1}{p_1}\right)\left(1-\frac{1}{p_2}\right)...\left(1-\frac{1}{p_k}\right).
$$

### 4.1.5A

投掷骰子相当于对骰子面上的六个数字进行有放回抽样。因此，我们可以使用问题 4.3 解决方案中给出的公式，该公式计算了从 $n$ 个对象中有放回地抽取 $s$ 次后，每个对象至少被抽取一次的概率 $\Theta(n,s)$。令 $n=6$ 代入该公式，我们可以看到，在 $s$ 次投掷中，数字 1-6 每个至少出现一次的概率为

![](img/eb401bf41900fd678cd9d368a197e486_365_0.png)

我们寻求满足 $\Theta(6, s) > 0.5$ 的最小 $s$ 值。通过尝试 $s = 1,2,3, \ldots$，我们最终发现 $\Theta(6,12) = 1,654,565/3,779,136$ 且 $\Theta(6,13) = 485,485/944,784$，因此 $\Theta(6,12) < 0.5 < \Theta(6,13)$，所以所需的 $s$ 值为 13。

### 4.1.6A

令 $\mathcal{A}_i$ 为那些不包含 $X_i$ 中任何元素的 $s$ 次抽样序列的集合。集合 $\bigcup_{i=1}^{n}X_i$ 中有 $np$ 个元素，总共有 $(np)^s$ 个 $s$ 个元素的序列。因此，一个 $s$ 次抽样序列包含每个集合 $X_i$ 中至少一个元素的概率，记为 $P$，为

![](img/eb401bf41900fd678cd9d368a197e486_365_1.png)

根据容斥原理，

![](img/eb401bf41900fd678cd9d368a197e486_365_2.png)

对于 $1 \le i_1 < i_2 < \ldots < i_k \le n$，集合 $\mathcal{A}_{i_1}\cap\mathcal{A}_{i_2}\cap\ldots\cap\mathcal{A}_{i_k}$ 由那些元素取自集合 $X_j$（其中 $j$ 不等于 $i_1, \ldots, i_k$）的 $s$ 次抽样序列组成，即取自这 $n-k$ 个集合中的某一个。因此，每个元素有 $(n-k)p$ 种选择。从而 $\#(\mathcal{A}_{i_1}\cap\mathcal{A}_{i_2}\cap\ldots\cap\mathcal{A}_{i_k}) = ((n-k)p)^s$。因此

![](img/eb401bf41900fd678cd9d368a197e486_365_3.png)

因此我们看到，概率确实与 $p$ 的值无关。

### 4.1.7A

根据练习 4.1.6A 的结果，在抽取 $s$ 张牌后，至少抽到 13 种牌点中每种牌点的一张牌的概率为 $\Theta(13, s)$，其表达式为 $\Theta(13,s) = \frac{1}{13^s}\sum_{k=0}^{13}(-1)^kC(13,k)(13-k)^s$。我们寻求满足 $\Theta(13, s) > 0.99$ 的最小 $s$ 值。计算机计算表明，所需的值为 $s = 90$。

### 4.2.1A

10 个对象的错排数为

![](img/eb401bf41900fd678cd9d368a197e486_365_4.png)

因此，所有 10 封信都放错信封的概率为

$$
\sum_{k=0}^{10} \frac{(-1)^k}{k!} = \frac{16,481}{44,800} \sim 0.368.
$$

### 4.2.2A

- i. \textit{ROBOT} 中的两个 $O$ 必须替换其他三个字母中的两个，且这对字母可以有三种选择方式。例如，考虑它们替换 \textit{R} 和 \textit{B} 的情况，此时我们有

  ![](img/eb401bf41900fd678cd9d368a197e486_366_0.png)

  那么 \textit{T} 的位置有两种选择，然后剩余的字母 \textit{R} 和 \textit{B} 可以以两种方式放置。因此，上述排列可以以 $2 \times 2 = 4$ 种方式完成。因此，\textit{ROBOT} 的变位词总共有 $3 \times 4 = 12$ 个。

- ii. 三个 \textit{A} 必须占据 \textit{G}、\textit{M}、\textit{N} 和 \textit{R} 这四个字母中三个的位置。因此，这些位置可以从 $C(4, 3) = 4$ 种方式中选出。集合 \{\textit{G}, \textit{M}, \textit{N}, \textit{R}\} 中未被 \textit{A} 替换的那个字母的位置可以有三种选择，因为它可以占据任意一个 \textit{A} 的位置。然后，该集合中剩余的三个字母可以以 $3!$ 种方式放置。因此，\textit{ANAGRAM} 的变位词总数为 $4 \times 3 \times 3! = 72$。

- iii. 我们根据哪个字母替换 \textit{T} 来考虑 \textit{TENNESSEE} 的变位词。
  - a. \textit{T} 被其中一个 \textit{N} 替换。那么四个 \textit{E} 必须替换 \textit{N} 和 \textit{S}，而剩余的 \textit{N}、\textit{S} 和 \textit{T} 必须替换 \textit{E}。\textit{N} 有四种可能的位置，然后 \textit{T} 有三种选择，因此有 $4 \times 3 = 12$ 个此类变位词。
  - b. \textit{T} 被其中一个 \textit{S} 替换。正如情况 (a) 中所述，此类变位词也有 12 个。
  - c. \textit{T} 被其中一个 \textit{E} 替换。我们根据 \textit{T} 现在替换哪个字母将此情况分为子情况。
    - $\alpha$. \textit{T} 替换其中一个 \textit{N}。这可以有两种方式发生。那么另一个 \textit{N} 和两个 \textit{S} 必须由剩余的 \textit{E} 替换。此时有 $C(4, 2) = 6$ 种方式使 2 个 \textit{N} 和 2 个 \textit{S} 替换 \textit{E}。因此此类变位词有 $2 \times 6 = 12$ 个。
    - $\beta$. \textit{T} 替换其中一个 \textit{S}。类似地，此类变位词也有 12 个。
    - $\gamma$. \textit{T} 替换其中一个 \textit{E}。这可以有四种方式发生。然后有四种方式使剩余的 \textit{E} 替换 \textit{N} 和 \textit{S}。如果一个 \textit{S} 没有被 \textit{E} 替换，那么它必须被 \textit{N} 替换，然后剩余的一个 \textit{N} 和两个 \textit{S} 有三种方式替换剩余的 \textit{E}。同样，如果一个 \textit{N} 没有被 \textit{E} 替换，剩余字母也有三种方式被替换。因此此类变位词有 $4 \times 12 = 48$ 个。

因此，总共有 $12 + 12 + (12 + 12 + 48) = 96$ 个不同的变位词。不幸的是，似乎没有更快的方法——但如果您找到了一种，请告诉我们。

### 4.3.1A

定理 4.5 中公式 4.7 给出

$$
S(4,2)=\frac{1}{2!}\sum_{s=0}^{1}(-1)^s C(2,s)(2-s)^4=\frac{1}{2!}\left[\left(C(2,0)2^4-C(2,1)1^4\right)\right]=\frac{1}{2!}(16-2)=7,
$$

并且也有

$$
\begin{align*}
S(8,4)&=\frac{1}{4!}\sum_{s=0}^{3}(-1)^s C(4,s)(4-s)^8=\frac{1}{4!}\left[\left(C(4,0)4^8-C(4,1)3^8+C(4,2)2^8-C(4,3)1^8\right)\right]\\
&=\frac{1}{4!}\frac{(65,536-26,244+1,536-4)}{24}=\frac{40,824}{24}=1,701,
\end{align*}
$$

两者均与表 3.2 中给出的值一致。

### 4.3.2A

由于 $S(1,1)=1$，该结果对 $n=1$ 成立。现在假设我们的归纳假设是对 $n=m$ 成立。设 $1 \leq k \leq m+1$。由于 $S(m+1, 1)=1$，当 $n=m+1$ 且 $k=1$ 时公式成立。因此，我们只需考虑 $2 \leq k \leq m+1$ 的情况。此时，利用定理 3.4 和归纳假设，我们有

$$
S(m+1,k)=S(m,k-1)+kS(m,k)=\frac{1}{(k-1)!}\sum_{s=0}^{k-2}(-1)^s C(k-1,s)(k-1-s)^m +\frac{k}{k!}\sum_{s=0}^{k-1}(-1)^s C(k,s)(k-s)^m.\tag{1}
$$

现在

$$
\sum_{s=0}^{k-2}(-1)^s C(k-1,s)(k-1-s)^m=\sum_{s=1}^{k-1}(-1)^{s-1} C(k-1,s-1)(k-s)^m.\tag{2}
$$

[不要被求和变量 $s$ 的范围变化所迷惑。要验证公式 2 是正确的，只需检查公式 1 的左边和右边都是以下表达式的不同写法：

$$
C(k-1,0)(k-1)^m-C(k-1,1)(k-2)^m+...+(-1)^{k-2}C(k-1,k-2)1^m.
$$]

