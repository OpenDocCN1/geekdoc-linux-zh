
### Definition 2.1

A point $w^*\in\mathbb{R}^n$ is called an equilibrium of (2.2), if and only if

$$
w^*=w^*+\eta\left[Cw^*-(w^*)^TCw^*w^*\right].
$$

Clearly, the set of all equilibrium points of (2.2) is

$$
\{v_1,\ldots,v_n\}\cup\{-v_1,\ldots,-v_n\}\cup\{0\}.
$$

## 2.3.3 Invariant Sets and Convergence Results

Some trajectories of (2.2) may diverge. Consider a simple example of a one dimensional equation.

$$
w(k+1)=w(k)+\eta\left[1-w^2(k)\right]w(k),\quad k\geq 0.
$$

If $w(k)\geq 1+1/\eta$, it holds that

$$
\eta w^2(k)-w(k)-\eta-1\geq 0.
$$

Then,

$$
|w(k+1)|=w^2(k)\cdot\frac{\eta w^2(k)-\eta-1}{w(k)}\geq w^2(k).
$$

Clearly, the trajectory approaches infinity if $w(0)\geq 1+1/\eta$. Other examples about divergence of Oja’s algorithm can be found in [210]. A problem to address is therefore to find out the conditions under which the trajectories can be bounded. The results forthcoming will be very important for applications. Next, we will prove an interesting theorem, which gives an invariant set of (2.2). The trajectories, thus, can be guaranteed to be bounded.

### Theorem 2.1

Denote

$$
S=\left\{w\mid w\in\mathbb{R}^n,\ w^T Cw\leq\frac{1}{\eta}\right\}.
$$

If

$$
\eta\sigma\leq\frac{3\sqrt[3]{2}-2}{2}\approx 0.8899,
$$

then $S$ is an invariant set of (2.2).

**Proof:** Given any $k\geq 0$, suppose $w(k)\in S$, that is,

$$
0\leq w^T(k)Cw(k)\leq\frac{1}{\eta}.
$$

Then,

$$
1+\eta\left(\lambda_i-w^T(k)Cw(k)\right)\geq\eta\lambda_i\geq 0,\quad(i=1,\ldots,n).
$$

From (2.2), (1.7), (1.8), and (2.3), it follows that

$$
\begin{aligned}
w^T(k+1)Cw(k+1)
&=\sum_{i=1}^{n}\lambda_i z_i^2(k+1)\\
&=\sum_{i=1}^{n}\lambda_i\left[1+\eta\left(\lambda_i-w^T(k)Cw(k)\right)\right]^2z_i^2(k)\\
&\leq\sum_{i=1}^{n}\lambda_i\left[1+\eta\left(\sigma-w^T(k)Cw(k)\right)\right]^2z_i^2(k)\\
&=\left[1+\eta\left(\sigma-w^T(k)Cw(k)\right)\right]^2w^T(k)Cw(k)\\
&\leq\max_{0\leq s\leq 1/\eta}\left\{\left[1+\eta(\sigma-s)\right]^2\cdot s\right\}\\
&\leq\max_{0\leq s\leq\sigma+1/\eta}\left\{\left[1+\eta(\sigma-s)\right]^2\cdot s\right\}.
\end{aligned}
$$

Using Lemma 2.1,

$$
w^T(k+1)Cw(k+1)\leq\frac{4}{27\eta}(1+\eta\sigma)^3.
$$

By

$$
\eta\sigma\leq\frac{3\sqrt[3]{2}-2}{2},
$$

it follows that

$$
\frac{4}{27\eta}(1+\eta\sigma)^3\leq\frac{1}{\eta}.
$$

Thus,

$$
w^T(k+1)Cw(k+1)\leq\frac{1}{\eta}.
$$

This shows that $w(k+1)\in S$, that is, $S$ is an invariant set. The proof is completed. Next, we will provide a deeper result, which will give a family of invariant sets.

### Theorem 2.2

Given any constant $l$ such that $1\leq l\leq 2$, if

$$
\eta\sigma\leq \frac{3\sqrt[3]{2l}-2}{2},
$$

then, the set

$$
S(l)=\left\{w\mid w\in\mathbb{R}^n,\;w^TCw\leq \lambda_p+\frac{l}{\eta}\right\}
$$

is an invariant set of (2.2).

**Proof:** Given any $k\geq 0$, suppose $w(k)\in S(l)$, we will prove that $w(k+1)\in S(l)$. Clearly,

$$
0\leq w^T(k)Cw(k)\leq \lambda_p+\frac{l}{\eta}.
$$

If

$$
\sigma\leq w^T(k)Cw(k)\leq \lambda_p+\frac{l}{\eta},
$$

then

$$
\begin{aligned}
\left[1+\eta\left(\lambda_i-w^T(k)Cw(k)\right)\right]^2
&=1+\eta^2\left(w^T(k)Cw(k)-\lambda_i\right)\left(w^T(k)Cw(k)-\lambda_i-\frac{2}{\eta}\right)\\
&\leq 1,\quad (i=1,\ldots,p).
\end{aligned}
$$

Thus,

$$
\begin{aligned}
w^T(k+1)Cw(k+1)
&=\sum_{i=1}^{n}\lambda_i z_i^2(k+1)\\
&=\sum_{i=1}^{p}\lambda_i z_i^2(k+1)\\
&=\sum_{i=1}^{p}\lambda_i\left[1+\eta\left(\lambda_i-w^T(k)Cw(k)\right)\right]^2z_i^2(k)\\
&\leq\sum_{i=1}^{p}\lambda_i z_i^2(k)\\
&=w^T(k)Cw(k)\\
&\leq\lambda_p+\frac{l}{\eta}.
\end{aligned}
$$

If

$$
0 \leq w^T(k)Cw(k) \leq \sigma,
$$

then it can be checked that

$$
\begin{aligned}
[1+\eta(\lambda_i-w^T(k)Cw(k))]^2
&\leq [1+\eta(\sigma-w^T(k)Cw(k))]^2,
\end{aligned}
$$

for $i=1,\ldots,n$. By Lemma 2.1,

$$
\begin{aligned}
w^T(k+1)Cw(k+1)
&=\sum_{i=1}^{n}\lambda_i[1+\eta(\lambda_i-w^T(k)Cw(k))]^2z_i^2(k)\\
&\leq [1+\eta(\sigma-w^T(k)Cw(k))]^2\cdot w^T(k)Cw(k)\\
&\leq \max_{0\leq s\leq \sigma}\{[1+\eta(\sigma-s)]^2s\}\\
&\leq \max_{0\leq s\leq \sigma<1/\eta}\{[1+\eta(\sigma-s)]^2s\}\\
&\leq \frac{4}{27\eta}(1+\eta\sigma)^3\\
&\leq \frac{l}{\eta}\\
&\leq \lambda_p+\frac{l}{\eta}.
\end{aligned}
$$

This shows that $w(k+1)\in S(l)$. The proof is completed.

Some invariant sets will follow from the above analysis. The nondivergence can thus be guaranteed by selecting initial vectors from the invariant sets. Next, we will further establish convergence results.

From (1.7), for each $k\geq 0$, $w(k)$ can be represented as

$$
w(k)=\sum_{i=1}^{m}z_i(k)v_i+\sum_{j=m+1}^{n}z_j(k)v_j,
$$

where $z_i(k)(i=1,\ldots,n)$ are some constants for each $k$. In particular,

$$
w(0)=\sum_{i=1}^{m}z_i(0)v_i+\sum_{j=m+1}^{n}z_j(0)v_j.
$$

Clearly, the convergence of $w(k)$ can be determined by the convergence of $z_i(k)(i=1,\ldots,m)$. Next, we analyze the convergence of $w(k)$ by studying the convergence of $z_i(k)(i=1,\ldots,m)$ and $z_i(k)(i=m+1,\ldots,n)$, respectively.

### Lemma 2.2

Suppose that

$$
\eta\sigma \le \frac{3\sqrt[3]{2}-2}{2}\approx 0.8899,
$$

if $w(0)\in S$ and $w(0)\notin V_{\sigma}^{\perp}$, then there exist constants $\theta_1>0$ and $\Pi_1\ge 0$ such that

$$
\sum_{j=m+1}^{n} z_j^2(k)\le \Pi_1\cdot e^{-\theta_1 k},
$$

for all $k\ge 0$, where

$$
\theta_1=\left[\ln\left(\frac{1+\eta\sigma}{1+\eta\lambda_{m+1}}\right)\right]^2>0.
$$

**Proof.** Since $w(0)\notin V_{\sigma}^{\perp}$, there must exist some $i\ (1\le i\le m)$ such that $z_i(0)\ne 0$. Without loss of generality, assume that $z_1(0)\ne 0$. From (2.3), it follows that

$$
z_i(k+1)=\left[1+\eta\left(\sigma-w^T(k)Cw(k)\right)\right]z_i(k),\quad 1\le i\le m, \tag{2.4}
$$

and

$$
z_j(k+1)=\left[1+\eta\left(\lambda_j-w^T(k)Cw(k)\right)\right]z_j(k),\quad m+1\le j\le n, \tag{2.5}
$$

for $k\ge 0$.

By Lemma 2.1, $S$ is an invariant set, then $w(k)\in S$ for all $k\ge 0$. Given any $i\ (1\le i\le n)$, it holds that

$$
1+\eta\left(\lambda_i-w^T(k)Cw(k)\right)=\eta\lambda_i+\left(1-\eta w^T(k)Cw(k)\right)\ge \eta\lambda_i>0,
$$

for $k\ge 1$. Then, from (2.4) and (2.5), for each $j\ (m+1\le j\le n)$, it follows that

$$
\begin{aligned}
\left[\frac{z_j(k+1)}{z_1(k+1)}\right]^2
&=\left[\frac{1+\eta\left(\lambda_j-w^T(k)Cw(k)\right)}{1+\eta\left(\sigma-w^T(k)Cw(k)\right)}\right]^2\left[\frac{z_j(k)}{z_1(k)}\right]^2\\
&\le \left[1-\frac{\eta(\sigma-\lambda_j)}{1+\eta\left(\sigma-w^T(k)Cw(k)\right)}\right]^2\left[\frac{z_j(k)}{z_1(k)}\right]^2\\
&\le \left(\frac{1+\eta\lambda_j}{1+\eta\sigma}\right)^2\left[\frac{z_j(k)}{z_1(k)}\right]^2\\
&\le \left(\frac{1+\eta\lambda_{m+1}}{1+\eta\sigma}\right)^2\left[\frac{z_j(k)}{z_1(k)}\right]^2\\
&=\left[\frac{z_j(0)}{z_1(0)}\right]^2\cdot e^{-\theta_1(k+1)},
\end{aligned}
$$

for all $k\ge 1$.

By the invariance of $S$, $z_1^2(k)$ must be bounded; that is, there exists a constant $d>0$ such that $z_1^2(k)\le d$ for all $k\ge 0$. Then,

$$
\sum_{j=m+1}^{n}z_j^2(k)=\sum_{j=m+1}^{n}\left[\frac{z_j(k)}{z_1(k)}\right]^2z_1^2(k)\le \Pi_1e^{-\theta_1k},
$$

for $k\ge 0$, where

$$
\Pi_1=d\sum_{j=m+1}^{n}\left[\frac{z_j(0)}{z_1(0)}\right]^2>0.
$$

This completes the proof.

### Lemma 2.3

Suppose that

$$
\eta\sigma\le\frac{3\sqrt[3]{2}-2}{2}\approx 0.8899.
$$

*If* $w(0)\in S$ and $w(0)\ne 0$, then

$$
\eta w^T(k+1)Cw(k+1)\ge\min\left\{(\eta\lambda_p)^3,\,w^T(0)Cw(0)\right\}
$$

for all $k\ge 0$.

**Proof.** Since $w(0)\in S$, by Theorem 2.1, $w(k)\in S$ for all $k\ge 0$, that is, $w^T(k)Cw(k)\le 1/\eta$, then

$$
1+\eta\left(\lambda_i-w^T(k)Cw(k)\right)\ge \eta\lambda_i\ge \eta\lambda_p>0,\qquad (i=1,\ldots,p),
$$

for all $k\ge 0$.

If $\lambda_p\le w^T(k)Cw(k)\le 1/\eta$, from (1.8) and (2.3), it follows that

$$
\begin{aligned}
\eta w^T(k+1)Cw(k+1)
&=\eta\sum_{i=1}^{n}\lambda_i z_i^2(k+1)\\
&=\eta\sum_{i=1}^{p}\lambda_i z_i^2(k+1)\\
&=\eta\sum_{i=1}^{p}\left[1+\eta\left(\lambda_i-w^T(k)Cw(k)\right)\right]^2\lambda_i z_i^2(k)\\
&\ge\left[\eta\lambda_p+\left(1-\eta w^T(k)Cw(k)\right)\right]^2\eta w^T(k)Cw(k)\\
&\ge(\eta\lambda_p)^2\eta w^T(k)Cw(k)\\
&\ge(\eta\lambda_p)^3 \tag{2.6}
\end{aligned}
$$

for $k\ge 0$.
