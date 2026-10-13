
Using the analysis of Case 1, Case 2, and Case 3, we complete the proof.

At this point, the boundedness of DDT system (5.4) has been proved.

Next, we prove that under some mild conditions,

$$\lim_{k\to\infty} w(k)=\pm v_n, \tag{5.14}$$

in (5.4), where $v_n$ is the minor component direction, that is, the unit eigenvector associated with the smallest eigenvalue of the covariance matrix. From (5.5), for each $k\geq 0$, $w(k)$ can be represented as

$$w(k)=\sum_{i=1}^{n-1}z_i(k)v_i+z_n(k)v_n, \tag{5.15}$$

where $z_i(k)\ (i=1,\ldots,n)$ are some constants. Clearly, the convergence of $w(k)$ can be determined by the convergence of $z_i(k)\ (i=1,\ldots,n)$. From (5.15), it can be observed that (5.14) can be obtained via proving the following two conclusions:

- **Conclusion 1:** $\lim_{k\to\infty}z_i(k)=0$, $(i=1,2,\ldots,n-1)$.
- **Conclusion 2:** $\lim_{k\to\infty}z_n(k)=\pm1$.

The following Lemma 5.3 and Lemma 5.4 will provide the proofs of *Conclusion 1* and *Conclusion 2*, respectively.

### **Lemma 5.3** Suppose that $\eta\lambda_1<0.25$, if $w(0)\in S$ and $w^T(0)v_n\neq 0$, then

$$\lim_{k\to\infty}z_i(k)=0,\quad(i=1,2,\ldots,n-1).$$

**Proof.** By $\eta\lambda_1<0.25$, it holds from (5.7) that

$$\begin{aligned}
\eta w^T(k)Cw(k)-0.25w^T(k)w(k)
&\leq \eta\lambda_1w^T(k)w(k)-0.25w^T(k)w(k)\\
&\leq 0.
\end{aligned} \tag{5.16}$$

Using Lemma 5.1, we have that for any $i\ (i=1,\ldots,n)$

$$1.5+(\eta\lambda_i-0.5)w^T(k)w(k)+\eta w^T(k)Cw(k)-2\eta\lambda_i\geq0, \tag{5.17}$$

for all $k\geq0$. Using Theorem 5.1, there must exist a constant $\zeta<2$ and a positive integer $N_1$ such that

$$\|w(k)\|^2\leq\zeta, \tag{5.18}$$

for all $k>N_1$. By $\eta\lambda_1<0.25$, it follows from (5.7), (5.16), (5.17), and (5.18) that for all $k\ge N$,

$$\begin{aligned}
&\frac{1.5+(\eta\lambda_i-0.5)w^T(k)w(k)+\eta w^T(k)Cw(k)-2\eta\lambda_i}{1.5+(\eta\lambda_n-0.5)w^T(k)w(k)+\eta w^T(k)Cw(k)-2\eta\lambda_n}\\
&\le \frac{1+(0.25-\eta\lambda_i)\cdot[2-w^T(k)w(k)]}{1+(0.25-\eta\lambda_n)\cdot[2-w^T(k)w(k)]}\\
&\le \frac{1+(0.25-\eta\lambda_i)\cdot(2-\zeta)}{1+(0.25-\eta\lambda_n)\cdot(2-\zeta)}\\
&\le \frac{1+(0.25-\eta\lambda_{n-1})\cdot(2-\zeta)}{1+(0.25-\eta\lambda_n)\cdot(2-\zeta)}\\
&=\gamma,\quad (i=1,2,\ldots,n-1),
\end{aligned} \tag{5.19}$$

where

$$\gamma=\frac{1+(0.25-\eta\lambda_{n-1})\cdot(2-\zeta)}{1+(0.25-\eta\lambda_n)\cdot(2-\zeta)}.$$

Since $\zeta<2$ and $\eta\lambda_1<0.25$, it holds that

$$0<\gamma<1. \tag{5.20}$$

By $w^T(0)v_n\ne 0$, clearly, $z_n(0)\ne 0$, and then $z_n(k)\ne 0\ (k>0)$. Using Lemma 5.1, it follows from (5.6) and (5.19) that

$$\begin{aligned}
\left[\frac{z_i(k+1)}{z_n(k+1)}\right]^2
&=\frac{1.5+(\eta\lambda_i-0.5)w^T(k)w(k)+\eta w^T(k)Cw(k)-2\eta\lambda_i}{1.5+(\eta\lambda_n-0.5)w^T(k)w(k)+\eta w^T(k)Cw(k)-2\eta\lambda_n}\left[\frac{z_i(k)}{z_n(k)}\right]^2\\
&\le \gamma^2\left[\frac{z_i(k)}{z_n(k)}\right]^2\\
&\le \gamma^{2(k-N+1)}\left[\frac{z_i(N)}{z_n(N)}\right]^2,\quad (i=1,2,\ldots,n-1).
\end{aligned}$$

for all $k\ge N$. From (5.20), clearly,

$$\lim_{k\to\infty}\frac{z_i(k)}{z_n(k)}=0,\quad (i=1,2,\ldots,n-1).$$

By the invariance of $S$, $z_n(k)$ must be bounded; then,

$$\lim_{k\to\infty}z_i(k)=0,\quad (i=1,2,\ldots,n-1).$$

The proof is completed.

### **Lemma 5.4** Suppose that $\eta\lambda_1<0.25$, if $w(0)\in S$ and $w^T(0)v_n\ne 0$, then it holds that

$$\lim_{k\to\infty}z_n(k)=\pm1.$$

**Proof.** Using Lemma 5.3, clearly, $w(k)$ will converge to the direction of the minor component direction $v_n$, as $k \to \infty$. Suppose at time $k_0$, $w(k)$ has converged to the direction of $v_n$, that is,

$$w(k_0)=z_n(k_0)\cdot v_n. \tag{5.21}$$

From (5.6), it holds that

$$\begin{aligned}
z_n(k+1) &= z_n(k)\cdot\left[(1.5-2\eta\lambda_n)+(2\eta\lambda_n-0.5)z_n^2(k)\right] \\
&= z_n(k)\cdot\left[1+(0.5-2\eta\lambda_n)(1-z_n^2(k))\right].
\end{aligned} \tag{5.22}$$

for all $k \geq k_0$. Since $w(0) \in S$, using Lemma 5.2, it holds that

$$|z_n(k)|^2 \leq \|w(k)\|^2 \leq 1+\frac{2}{1-4\eta\lambda_n}.$$

for all $k \geq 0$. By $\eta\lambda_1<0.25$, clearly,

$$1+(0.5-2\eta\lambda_n)(1-z_n^2(k))>0. \tag{5.23}$$

for all $k \geq 0$. Thus, from (5.22) and (5.23), it holds that

$$|z_n(k+1)|=|z_n(k)|\cdot\left[1+(0.5-2\eta\lambda_n)(1-z_n^2(k))\right], \tag{5.24}$$

for all $k \geq k_0$. By $\eta\lambda_1<0.25$, then

$$\frac{|z_n(k+1)|}{|z_n(k)|}=1+(0.5-2\eta\lambda_n)\left[1-z_n^2(k)\right]=\begin{cases}>1, & \text{if } |z_n(k)|<1,\\=1, & \text{if } |z_n(k)|=1,\\<1, & \text{if } |z_n(k)|>1.\end{cases} \tag{5.25}$$

for all $k \geq k_0$. From (5.25), clearly, $|z_n(k)|=1$ is a potential stable equilibrium point of (5.24). Next, three cases will be considered to complete the proof.

**Case 1:** $|z_n(k_0)|\leq 1$.

By $\eta\lambda_n\le\eta\lambda_1<0.25$ and $|z_n(k_0)|\leq 1$, it can be calculated out from (5.24) that

$$|z_n(k_0+1)|=(2\eta\lambda_n-0.5)|z_n(k_0)|^3+(1.5-2\eta\lambda_n)|z_n(k_0)|\leq 1.$$

Clearly, it holds that $|z_n(k)|\leq 1$ for all $k\geq k_0$. However, it holds from (5.25) that $|z_n(k)|$ is monotone increasing for all $k\geq k_0$. Thus, $|z_n(k)|$ must converge to the equilibrium point 1, as $k\to\infty$.

**Case 2:** $|z_n(k)|>1$ for all $k\geq k_0$.

From (5.25), it holds that $|z_n(k)|$ is monotone decreasing for all $k\geq k_0$. However, $|z_n(k)|$ has a lower bound 1 for all $k\geq k_0$. Clearly, $|z_n(k)|$ will converge to the equilibrium point 1, as $k\to\infty$.

**Case 3:** $|z_n(k_0)|>1$, and there exists a positive integer $M\ (M>k_0)$, such that $|z_n(M)|\leq 1$.

Since $|z_n(M)|\leq 1$, in the same way as Case 1, it can be proved that $|z_n(k)|$ must converge to the equilibrium point 1, as $k\to\infty$.

From the analysis of the previous three cases, we can obtain that

$$\lim_{k\to\infty}|z_n(k)|=1. \tag{5.26}$$

At the same time, from (5.22) and (5.23), we have that, if $z_n(k_0)\ge 0$, then $z_n(k)>0$ for all $k>k_0$, or if $z_n(k_0)\le 0$, then $z_n(k)\le 0$ for all $k>k_0$. Thus, it holds from (5.26) that

$$\lim_{k\to\infty}z_n(k)=\pm 1.$$

This completes the proof.

In Lemma 5.3, we have proved that if $\eta\lambda_1<0.25$, $w(0)\in S$, and $w^T(0)v_n\ne 0$, then

$$\lim_{k\to\infty}z_i(k)=0,\quad (i=1,2,\ldots,n-1). \tag{5.27}$$

In Lemma 5.4, it is proved that if $\eta\lambda_1<0.25$, $w(0)\in S$, and $w^T(0)v_n\ne 0$, then

$$\lim_{k\to\infty}z_n(k)=\pm 1. \tag{5.28}$$

Since

$$w(k)=\sum_{i=1}^{n-1}z_i(k)v_i+z_n(k)v_n,$$

from (5.27) and (5.28), we can easily draw the following conclusion:

### **Theorem 5.2** *if $\eta\lambda_1<0.25$, $w(0)\in S$, and $w^T(0)v_n\ne 0$, then in (5.4),*

$$\lim_{k\to\infty}w(k)=\pm v_n.$$

At this point, we have finished the proof of convergence of DDT system (5.4). Next, we further study the stability of (5.4). Clearly, the set of all equilibrium points of (5.4) is

$$\{v_1,\ldots,v_n\}\cup\{-v_1,\ldots,-v_n\}\cup\{0\}.$$

The following Theorem 5.3 will show the stability of the equilibrium points $v_n$ and $-v_n$ in (5.4).

### **Theorem 5.3** *The equilibrium points $v_n$ and $-v_n$ are locally asymptotically stable if*

$$\eta\lambda_1<0.25.$$

*Other equilibrium points of (5.4) are unstable.*

**Proof.** Denote

$$\begin{aligned}
G(w)&=w(k+1)\\
&=w(k)+\eta\left[(w^T(k)w(k)-2)Rw(k)+w^T(k)Rw(k)w(k)\right]\\
&\quad+0.5\left[1-w^T(k)w(k)\right]w(k).
\end{aligned}$$

Then, it follows that

$$\left.\frac{\partial G}{\partial w}\right|_{0}=I+2\eta C-\eta w^{T}(k)w(k)C-\eta w^{T}(k)Cw(k)I-4\eta Cw(k)w^{T}(k), \tag{5.29}$$

where

$$C=\frac{1}{4\eta}I-R,$$

and $I$ is the unity matrix. For the equilibrium point $0$, it holds from (5.29) that

$$\left.\frac{\partial G}{\partial w}\right|_{0}=I+2\eta C=1.5I-2\eta R=J_0.$$

Denote the $i$th eigenvalue of $J_0$ by $\alpha_0^{(i)}$. By $\eta\lambda_1<0.25$, it holds that

$$\alpha_0^{(i)}=1.5-2\eta\lambda_i\ge 1.5-2\eta\lambda_1>1,\quad (i=1,2,\ldots,n).$$

According to the Lyapunov theory, the equilibrium point $0$ is unstable.

For the equilibrium points $\pm v_j$ $(j=1,\ldots,n)$, it follows from (5.29) that

$$\left.\frac{\partial G}{\partial w}\right|_{v_j}=(1+\eta\lambda_j)I-\eta R-(1-4\eta\lambda_j)v_jv_j^T=J_j.$$

Denote the $i$th eigenvalue of $J_j$ by $\alpha_j^{(i)}$. Clearly,

$$\alpha_j^{(i)}=1+\eta(\lambda_j-\lambda_i)\quad\text{if }i\ne j.$$

$$\alpha_j^{(j)}=4\eta\lambda_j\quad\text{if }i=j.$$

For any $j\ne n$, it holds that

$$\alpha_j^{(n)}=1+\eta(\lambda_j-\lambda_n)>1.$$

Clearly, the equilibrium points $\pm v_j$ $(j\ne n)$ are unstable. For the equilibrium points $\pm v_n$, since $\eta\lambda_1<0.25$, it follows that

$$\alpha_n^{(i)}=1+\eta(\lambda_n-\lambda_i)<1\ \text{if }i\ne n.$$

$$\alpha_n^{(i)}=4\eta\lambda_n<4\eta\lambda_1<1\ \text{if }i=n.$$

Thus, $\pm v_n$ are asymptotically stable. The proof is completed.

In this section, we have analyzed the dynamics of DDT system (5.4) associated with the proposed stable MCA learning algorithm (5.3) and proved that the weight vector of (5.4) will converge to stable equilibrium points $\pm v_n$ under some conditions.
