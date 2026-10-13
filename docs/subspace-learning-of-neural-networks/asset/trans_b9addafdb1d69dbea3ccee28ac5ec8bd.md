

\[
\theta_1=\ln\left(\frac{(1+\eta a)(a+3b)}{(1+\eta a)(a+3b)+\eta ab\bar p\,\operatorname{Kurt}(s_i)}\right)^2>0.
\]

**证明。** 由于 \(z(0)\notin V_q^1\)，必定存在 \(j\in Q\)，使得 \(z_j(0)\ne 0\)。对于任意 \(z_i(k)\ne 0\)，\(i\in P\)，且对所有 \(k\ge 0\) 有 \(z_i^2(k)>\bar p>0\)，由 (6.7) 可得

\[
\left[\frac{z_i(k+1)}{z_j(k+1)}\right]^2=
\left[\frac{1+\eta a-\eta a\|z(k)\|^2+\eta b\bigl(\operatorname{Kurt}(s_i(k))z_i^2(k)+3\|z(k)\|^2\bigr)}{1+\eta a-\eta a\|z(k)\|^2+\eta b\bigl(\operatorname{Kurt}(s_j(k))z_j^2(k)+3\|z(k)\|^2\bigr)}\right]^2\cdot
\left[\frac{z_i(k)}{z_j(k)}\right]^2,
\]

对所有 \(k\ge 0\) 成立。由引理 6.5 以及 \(i\in P\)，即 \(\operatorname{Kurt}(s_i)<0\)，可得

\[
\left[\frac{z_i(k+1)}{z_j(k+1)}\right]^2
\leq
\left[\frac{1+\eta a-\eta a\|z(k)\|^2+\eta b\bigl(\operatorname{Kurt}(s_i(k))\bar p+3\|z(k)\|^2\bigr)}{1+\eta a-\eta a\|z(k)\|^2+3\eta b\|z(k)\|^2}\right]^2\cdot
\left[\frac{z_i(k)}{z_j(k)}\right]^2
\]

\[
\leq
\left[\frac{1+\eta a+\eta b\bar p\,\operatorname{Kurt}(s_i)+3\eta b\|z(k)\|^2}{1+\eta a+3\eta b\|z(k)\|^2}\right]^2\cdot
\left[\frac{z_i(k)}{z_j(k)}\right]^2,
\]

对所有 \(k\ge 0\) 成立。由于 \(\|z(k)\|^2<\frac{1+\eta a}{\eta a}\)，由引理 6.2 可得

\[
\left[\frac{z_i(k+1)}{z_j(k+1)}\right]^2
\leq
\left[\frac{1+\eta a+\eta b\bar p\,\operatorname{Kurt}(s_i)+3\eta b\cdot\frac{1+\eta a}{\eta a}}{1+\eta a+3\eta b\|z(k)\|^2}\right]^2\cdot
\left[\frac{z_i(k)}{z_j(k)}\right]^2
\]

\[
\leq
\left[\frac{(1+\eta a)(a+3b)+\eta ab\bar p\,\operatorname{Kurt}(s_i)}{(1+\eta a)(a+3b)}\right]^2\cdot
\left[\frac{z_i(k)}{z_j(k)}\right]^2
\]

\[
\leq
\left[\frac{(1+\eta a)(a+3b)+\eta ab\bar p\,\operatorname{Kurt}(s_i)}{(1+\eta a)(a+3b)}\right]^{2(k+1)}\cdot
\left[\frac{z_i(0)}{z_j(0)}\right]^2
\]

\[
=\left[\frac{z_i(0)}{z_j(0)}\right]^2\cdot e^{-\theta_1(k+1)},
\]

对所有 \(k\ge 0\) 成立，其中

\[
\theta_1=\ln\left(\frac{(1+\eta a)(a+3b)}{(1+\eta a)(a+3b)+\eta ab\bar p\,\operatorname{Kurt}(s_i)}\right)^2>0.
\]

由于 \(z(0)\in S_{z_1}\)，有

\[
|z_i(k+1)|^2\leq |z_j(k+1)|^2\cdot\left[\frac{z_i(0)}{z_j(0)}\right]^2\cdot e^{-\theta_1 k}<\Pi_1\cdot e^{-\theta_1 k},
\]

其中

\[
\Pi_1=\frac{1+\eta a}{\eta a}\cdot\left[\frac{z_i(0)}{z_j(0)}\right]^2.
\]

证毕。

### 引理 6.7

假设 \(\operatorname{Kurt}(s_{j_0})>0\)（\(j_0\in Q\)），且 \(\operatorname{Kurt}(s_j)\ge 0\)，\(j\in(Q\cup O)/j_0\)。如果 \(\operatorname{Kurt}(s_{j_0})z_{j_0}^2(0)>\operatorname{Kurt}(s_j)z_j^2(0)\)，则必定存在常数 \(\xi>0\)，使得对所有 \(k\ge 0\) 有 \(0<\psi(k)<1\)，其中

\[
\psi(k)=\left[\frac{(1+\eta a)(a+3b)+\eta b\operatorname{Kurt}(s_j)z_j^2(k)}{(1+\eta a)(a+3b)+\eta b\operatorname{Kurt}(s_{j_0})z_{j_0}^2(k)}\right]^2.
\]

**证明。** 对于 \(j_0\in Q\) 以及任意 \(j\in(Q\cup O)/j_0\)，由 (6.7) 可得

\[
\frac{z_j^2(k+1)}{z_{j_0}^2(k+1)}=\gamma(k)\frac{z_j^2(k)}{z_{j_0}^2(k)},\tag{6.8}
\]

对所有 \(k\ge 0\) 成立，其中

\[
\gamma(k)=\left[\frac{1+\eta a-\eta a\|z(k)\|^2+\eta b\bigl(\operatorname{Kurt}(s_j)z_j^2(k)+3\|z(k)\|^2\bigr)}{1+\eta a-\eta a\|z(k)\|^2+\eta b\bigl(\operatorname{Kurt}(s_{j_0})z_{j_0}^2(k)+3\|z(k)\|^2\bigr)}\right]^2.
\]

如果 \(\operatorname{Kurt}(s_{j_0})z_{j_0}^2(k)>\operatorname{Kurt}(s_j)z_j^2(k)\ge 0\)，由引理 6.5 可知 \(0<\gamma(k)<1\)。由 (6.8) 可得

\[
z_{j_0}^2(k+1)z_j^2(k)>z_j^2(k+1)z_{j_0}^2(k)\ge 0.
\]

因此，容易看出

\[
\operatorname{Kurt}(s_{j_0})z_{j_0}^2(k+1)>\operatorname{Kurt}(s_j)z_j^2(k+1)\ge 0.
\]

于是，如果 \(\operatorname{Kurt}(s_{j_0})z_{j_0}^2(0)>\operatorname{Kurt}(s_j)z_j^2(0)\ge 0\)，则有

\[
\operatorname{Kurt}(s_{j_0})z_{j_0}^2(k+1)>\operatorname{Kurt}(s_j)z_j^2(k+1),\tag{6.9}
\]

对所有 \(k\ge 0\) 成立。

现在，我们将证明：如果 \(\operatorname{Kurt}(s_{j_0})z_{j_0}^2(0)>\operatorname{Kurt}(s_j)z_j^2(0)\ge 0\)，则必定存在一个小的常数 \(\epsilon>0\)，使得对所有 \(k\ge 0\) 有 \(z_{j_0}^2(k)>\epsilon\)。假设这不成立，则有 \(\lim_{k\to+\infty}z_{j_0}^2(k)=0\)。由 (6.9) 可得 \(\lim_{k\to+\infty}z_j^2(k)=0\)，\(j\in(Q\cup O)/j_0\)。由引理 6.6，有

\[
\lim_{k\to+\infty}\|z(k)\|^2=0.
\]

这与定理 6.2 矛盾。

由于 \(\operatorname{Kurt}(s_{j_0})z_{j_0}^2(0)>\operatorname{Kurt}(s_j)z_j^2(0)\ge 0\) 且对所有 \(k\ge 0\) 有 \(0<\gamma(k)<1\)，由 (6.8) 可得

\[
\operatorname{Kurt}(s_{j_0})z_{j_0}^2(k+1)-\operatorname{Kurt}(s_j)z_j^2(k+1)
\]

\[
=\operatorname{Kurt}(s_{j_0})z_{j_0}^2(k+1)\left(1-\gamma(k)\frac{\operatorname{Kurt}(s_j)z_j^2(k)}{\operatorname{Kurt}(s_{j_0})z_{j_0}^2(k)}\right)
\]

\[
=\operatorname{Kurt}(s_{j_0})z_{j_0}^2(k+1)\left(1-\prod_{l=1}^{k}\gamma(l)\cdot\frac{\operatorname{Kurt}(s_j)z_j^2(0)}{\operatorname{Kurt}(s_{j_0})z_{j_0}^2(0)}\right)
\]

\[
>\operatorname{Kurt}(s_{j_0})z_{j_0}^2(k+1)\left(1-\frac{\operatorname{Kurt}(s_j)z_j^2(0)}{\operatorname{Kurt}(s_{j_0})z_{j_0}^2(0)}\right),
\]

对所有 \(k\ge 0\) 成立。由此可得

\[
\eta ab\operatorname{Kurt}(s_{j_0})z_{j_0}^2(k+1)-\eta ab\operatorname{Kurt}(s_j)z_j^2(k+1)>\bar\epsilon>0,
\]

其中

\[
\bar\epsilon=\eta ab\operatorname{Kurt}(s_{j_0})\epsilon\left(1-\frac{\operatorname{Kurt}(s_j)z_j^2(0)}{\operatorname{Kurt}(s_{j_0})z_{j_0}^2(0)}\right).
\]

容易证明

\[
\xi=1-\frac{a\bar\epsilon}{(1+\eta a)[a(a+3b)+\eta ab\operatorname{Kurt}(s_{j_0})]}<1,
\]

且

\[
\psi(k)=\frac{(1+\eta a)(a+3b)+\eta ab\operatorname{Kurt}(s_j)z_j^2(k)}{(1+\eta a)(a+3b)+\eta ab\operatorname{Kurt}(s_{j_0})z_{j_0}^2(k)}<\xi,
\]

对所有 \(k\ge 0\) 成立。证毕。

### 引理 6.8

假设 \(z(0)\in S_{\bar{1}}\)，\(z(0)\notin V_1^{\perp}\)，且 \(\Gamma_z\ge\max\{\operatorname{Kurt}(s_j)+3,3\}\)。如果 \(\operatorname{Kurt}(s_{j_0})z_{j_0}^{2}(0)>\operatorname{Kurt}(s_j)z_j^{2}(0)\ge 0\)，其中 \(j_0\in Q\)，\(j\in(Q\cup O)/j_0\)，则有

\[
|z_j(k+1)|^2\leq |z_{j_0}(k+1)|^2\cdot\left[\frac{z_j(0)}{z_{j_0}(0)}\right]^2\cdot e^{-\theta_2 k}<\Pi_2\cdot e^{-\theta_2 k},
\]

对所有 \(j\in(Q\cup O)/j_0\) 成立，其中

\[
\Pi_2=\frac{1+\eta a}{\eta a}\cdot\left[\frac{z_j(0)}{z_{j_0}(0)}\right]^2,\qquad
\theta_2=\ln\left[\frac{1}{\xi}\right]^2>0.
\]

**证明。** 由于 \(z(0)\notin V_1^{\perp}\)，必定存在 \(j_0\)（\(j_0\in Q\)），使得 \(z_{j_0}(0)\ne 0\)，且 \(\operatorname{Kurt}(s_{j_0})z_{j_0}^{2}(0)>\operatorname{Kurt}(s_j)z_j^{2}(0)\)，\(j\in Q/j_0\)。由 (6.7) 可得

\[
\frac{z_j^2(k+1)}{z_{j_0}^2(k+1)}=
\left[\frac{1+\eta a-\eta a\|z(k)\|^2+\eta b\left(\operatorname{Kurt}(s_j(k))z_j^2(k)+3\|z(k)\|^2\right)}{1+\eta a-\eta a\|z(k)\|^2+\eta b\left(\operatorname{Kurt}(s_{j_0}(k))z_{j_0}^2(k)+3\|z(k)\|^2\right)}\right]^2
\cdot\frac{z_j^2(k)}{z_{j_0}^2(k)}.
\]

由引理 6.2 和引理 6.7，有

\[
\frac{z_j^2(k+1)}{z_{j_0}^2(k+1)}\leq\xi\frac{z_j^2(k)}{z_{j_0}^2(k)},
\]

对所有 \(k\ge 0\) 成立。因此可得

\[
|z_j(k+1)|^2\leq |z_{j_0}(k+1)|^2\cdot\left[\frac{z_j(0)}{z_{j_0}(0)}\right]^2\cdot e^{-\theta_2 k}<\Pi_2\cdot e^{-\theta_2 k},
\]

对所有 \(j\in(Q\cup O)/j_0\) 成立，其中

\[
\Pi_2=\frac{1+\eta a}{\eta a}\cdot\left[\frac{z_j(0)}{z_{j_0}(0)}\right]^2,\qquad
\theta_2=\ln\left[\frac{1}{\xi}\right]^2>0.
\]

证毕。

### 引理 6.9

假设 \(z(0)\in S_{\Sigma_1}\)，\(z(0)\notin V_l^1\)，且 \(\Gamma_{\Sigma}>\max\{\operatorname{Kurt}(s_i)+3,3\}\)。如果 \(\operatorname{Kurt}(s_{j_0})z_{j_0}^2(0)>\operatorname{Kurt}(s_j)z_j^2(0)\)，其中 \(j_0\in Q\)，\(j\in I/j_0\)，则有

\[
\eta a-V(k+1)<\zeta^k\cdot[\eta a-V(0)],
\]

其中 \(V(k)=\eta[a-b(\operatorname{Kurt}(s_{j_0})+3)]z_{j_0}^2(k)\)，\(\zeta=\max\{|(1-\gamma)^2-\eta a\gamma|,\ |1-2\eta a|\}\)，当 \(k\) 足够大时成立。

**证明。** 由引理 6.6 和引理 6.8 可得

\[
\lim_{k\to+\infty}z_i(k)=0,\quad(i\in P\text{ 且 }\operatorname{Kurt}(s_i)<0),
\]

\[
\lim_{k\to+\infty}z_j(k)=0,\quad(j\in(Q\cup O)/j_0\text{ 且 }\operatorname{Kurt}(s_j)\ge 0),
\]

其中 \(j_0\in Q\)，\(\operatorname{Kurt}(s_{j_0})z_{j_0}^2(0)>\operatorname{Kurt}(s_j)z_j^2(0)\)。由 (6.7)，当 \(k\) 足够大时，可得

\[
z_{j_0}(k+1)=z_{j_0}(k)+[\eta a-\eta a z_{j_0}^2(k)+\eta b(\operatorname{Kurt}(s_{j_0})z_{j_0}^2(k)+3z_{j_0}^2(k))]z_{j_0}(k)
\]

\[
\qquad=\{1+\eta a-\eta[a-b(\operatorname{Kurt}(s_{j_0})+3)]z_{j_0}^2(k)\}z_{j_0}(k).
\]

由于 \(z(0)\in S_{\Sigma_1}\)，必定存在一个小的常数 \(\varrho\)，使得 \(0<\varrho<1\) 且 \(\varrho\le V(k)\)。因此，可以验证

\[
0<\varrho<V(k)\le \eta[a-b(\operatorname{Kurt}(s_{j_0})+3)]\frac{1+\eta a}{\eta a}
\]

\[
\qquad=\frac{a-b(\operatorname{Kurt}(s_{j_0})+3)}{a}(1+\eta a)
\]

\[
\qquad\le 2,
\]

其中 \(0<\eta a<1\)，且 \(a>b(\operatorname{Kurt}(s_{j_0})+3)\)。进而可得

\[
\eta a-V(k+1)=\eta a-\eta[a-b(\operatorname{Kurt}(s_{j_0})+3)]z_{j_0}^2(k+1)
\]

\[
\qquad=\eta a-\eta[a-b(\operatorname{Kurt}(s_{j_0})+3)]\cdot
\]

\[
\qquad\qquad\{1+\eta a-\eta[a-b(\operatorname{Kurt}(s_{j_0})+3)]z_{j_0}^2(k)\}^2z_{j_0}^2(k).
\]

容易得到

\[
\eta a-V(k+1)=[\eta a-V(k)]\{[1-V(k)]^2-\eta aV(k)\}
\]

\[
\qquad\le |\eta a-V(k)|\,|[1-V(k)]^2-\eta aV(k)|.
\]

由引理 6.3 可得

\[
|\eta a-V(k+1)|\le |\eta a-V(k)|\cdot|[1-V(k)]^2-\eta aV(k)|
\]

\[
\qquad\le |\eta a-V(k)|\cdot\zeta
\]

\[
\qquad=\zeta^k|\eta a-V(0)|,
\]

其中 \(0<\zeta<1\)。证毕。

