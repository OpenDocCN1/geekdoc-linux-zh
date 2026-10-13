
determines whether we are minimizing or maximizing the kurtosis. \(\mu(k)\) is the learning rate sequence and \(\boldsymbol{x}(k)\) is a prewhitened input data. In this chapter, let \(f(y)=y^3\), and the constant learning rates are used. The algorithms with constant learning rates can be presented as

$$\boldsymbol{w}(k+1)=\boldsymbol{w}(k)+\eta\left[b_x(k)\boldsymbol{x}(k)(\boldsymbol{w}^{T}(k)\boldsymbol{x}(k))^3+a(1-\|\boldsymbol{w}(k)\|^2)\boldsymbol{w}(k)\right]. \tag{6.1}$$

$$\boldsymbol{w}(k+1)=\boldsymbol{w}(k)+\eta\left[-b_x(k)\boldsymbol{x}(k)(\boldsymbol{w}^{T}(k)\boldsymbol{x}(k))^3+a(1-\|\boldsymbol{w}(k)\|^2)\boldsymbol{w}(k)\right]. \tag{6.2}$$

for all \(k\geq 0\), where \(\eta\) is a constant learning rate. A constant \(b\geq 0\) is added to the algorithms to adjust the learning parameters more conveniently.

The algorithm (6.1) converges to an independent component direction with a positive kurtosis, that is, \(\boldsymbol{w}(k)\) will converge to a direction of a column \(\boldsymbol{b}_i\) of \(B\) with \(\operatorname{Kurt}(s_i)>0\). The algorithm (6.2) converges to an independent component direction with a negative kurtosis, that is, \(\boldsymbol{w}(k)\) will converge to a direction of a column \(\boldsymbol{b}_i\) of \(B\) with \(\operatorname{Kurt}(s_i)<0\).

To prove the convergence of the algorithms, a transformation is given first. Let \(\boldsymbol{w}(k)=B\tilde{\boldsymbol{z}}(k)\). Clearly, to prove that \(\boldsymbol{w}(k)\) converges to a direction of a column \(\boldsymbol{b}_i\) of \(B\), it only needs to prove that all components of \(\tilde{\boldsymbol{z}}(k)\) converge to zero except \(\tilde{z}_i(k)\). Since \(\boldsymbol{x}(k)=B\boldsymbol{s}(k)\), from (6.1) and (6.2), it follows that

$$\tilde{\boldsymbol{z}}(k+1)=\tilde{\boldsymbol{z}}(k)+\eta\left[b_s(k)\boldsymbol{s}(k)(\tilde{\boldsymbol{z}}^{T}(k)\boldsymbol{s}(k))^3+a(1-\|\tilde{\boldsymbol{z}}(k)\|^2)\tilde{\boldsymbol{z}}(k)\right]. \tag{6.3}$$

$$\tilde{\boldsymbol{z}}(k+1)=\tilde{\boldsymbol{z}}(k)+\eta\left[-b_s(k)\boldsymbol{s}(k)(\tilde{\boldsymbol{z}}^{T}(k)\boldsymbol{s}(k))^3+a(1-\|\tilde{\boldsymbol{z}}(k)\|^2)\tilde{\boldsymbol{z}}(k)\right]. \tag{6.4}$$

for all \(k\geq 0\).

In the following section, the convergence of the Hyvärinen-Oja algorithms will be analyzed in detail. First, some lemmas are provided to be used for subsequent analysis.

**Lemma 6.1** Suppose that \(D>0\), \(E>0\). It holds that

$$[D-Eh]^2\cdot h\leq\frac{4D^3}{27E}.$$

for all \(0<h\leq\frac{D}{E}\).

*Proof.* Define a differentiable function

$$f(h)=[D-Eh]^2\cdot h.$$

for \(0<h<\frac{D}{E}\). It follows that \(f'(h)=[D-Eh]\cdot[D-3Eh]\). It is easy to get the maximum point of \(f(h)\) on the interval \((0,\frac{D}{E})\) must be \(h=\frac{D}{3E}\). Thus, it follows that

$$[D-Eh]^2\cdot h\leq\frac{4D^3}{27E},$$

where \(0<h<\frac{D}{E}\). The proof is complete.

**Lemma 6.2** Suppose \(H>F>0\). If \(N>C>0\), then

$$\frac{F+C}{H+C}<\frac{F+N}{H+N}.$$

*Proof.* It holds that

$$\frac{F+C}{H+C}-\frac{F+N}{H+N}=\frac{(F-H)(N-C)}{(H+C)(H+N)}<0.$$

The proof is complete.

**Lemma 6.3** Suppose \(0<\varrho<1\). If \(0<\eta a<1\) and \(\varrho\le h\le 2\), it holds that

$$\left|(1-h)^2-\eta ah\right|\le\zeta,$$

where \(\zeta=\max\{|(1-\varrho)^2-\eta a\varrho|,|1-2\eta a|\}\) and \(0<\zeta<1\).

*Proof.* Define a differentiable function

$$f(h)=(1-h)^2-\eta ah,$$

for all \(\varrho\le h\le 2\), where \(0<\eta a<1\). It follows that \(f'(h)=-2(1-h)-\eta a\). It is easy to get the maximum of \(f(h)\) on the interval \([\varrho,2]\) is attained at \(h=\varrho\) or \(h=2\). Thus, it follows that

$$\left|(1-h)^2-\eta ah\right|\le\zeta,$$

where \(\zeta=\max\{|(1-\varrho)^2-\eta a\varrho|,|1-2\eta a|\}<1\). The proof is complete.

## 6.3 Convergence Analysis

The algorithms (6.1) and (6.2) may diverge. Consider one-dimensional examples. From (6.1), it follows that

$$w(k+1)=w(k)+\eta\left[bw^3(k)x^4(k)+a\left(1-w^2(k)\right)w(k)\right]$$
$$=\left[1+\eta a-\eta\left(a-bx^4(k)\right)w^2(k)\right]w(k),$$

where \(\eta>0\), \(a>0\) and \(b>0\). Suppose \(a-bx^4(k)>\bar a>0\) for all \(k\ge 0\), where \(\bar a\) is a constant. If \(w(k)>\frac{1+\eta a}{\eta\bar a}\), it holds that \(\eta\left(a-bx^4(k)\right)w^2(k)-w(k)-\eta a-1>0\). It follows that

$$|w(k+1)|=w^2(k)\frac{\eta\left(a-bx^4(k)\right)w^2(k)-\eta a-1}{w(k)}$$
$$>w^2(k),$$

for all \(k \ge 0\). Thus, the trajectory approaches toward infinity if \(w(0)>\dfrac{1+\eta a}{\eta\bar a}\) under the condition \(a-bx^4(k)>\bar a\) for all \(k\ge 0\). From (6.2), it follows that

$$w(k+1)=w(k)+\eta[-bw^3(k)x^4(k)+a(1-w^2(k))w(k)]$$
$$=[1+\eta a-\eta(a+bx^4(k))w^2(k)]w(k),$$

where \(\eta>0\), \(a>0\) and \(b>0\). If \(w(k)>\dfrac{1+\eta a}{\eta a}\), it holds that \(\eta(a+bx^4(k))w^2(k)-w(k)-\eta a-1>0\). It follows that

$$|w(k+1)|=w^2(k)\frac{\eta(a+bx^4(k))w^2(k)-\eta a-1}{w(k)}$$
$$>w^2(k),$$

for all \(k\ge 0\). Thus, the trajectory approaches toward infinity if \(w(0)>\dfrac{1+\eta a}{\eta a}\).

The preceding examples show the algorithms (6.1) and (6.2) may diverge. A problem to address is therefore to find the conditions under which the algorithms are bounded. In the following section, by directly studying the SDT algorithms (6.1) and (6.2), some interesting theorems are given to guarantee the nondivergence of the algorithms in stochastic environment.

### 6.3.1 Invariant Sets

Let \(\Gamma_w=\sup\{\|\boldsymbol{x}(k)\|^4,k=1,2,\ldots\}\), assume \(\Gamma_w\) is finite and \(\|\boldsymbol{w}(0)\|^2\ne 0\). Suppose \(\|\boldsymbol{w}(0)\|^2\le\dfrac{1+\eta a}{\eta a}\). Define

$$M_{w1}=\min\left\{\delta_{w1}\left[G-\eta(a-b\Gamma_w)\|\boldsymbol{w}(0)\|^2\right]\|\boldsymbol{w}(0)\|^2,\ \delta_{w1}\frac{(b\Gamma_w+\eta b\Gamma_w)^2G}{\eta a^3}\right\},$$

where \(G=1+\eta a\), \(a>b\Gamma_w\), and \(\delta_{w1}>0\) is a small constant. Clearly, \(M_{w1}>0\).

Suppose \(\|\boldsymbol{w}(0)\|^2\le\dfrac{1+\eta a}{\eta a+\eta b\Gamma_w}\). Define

$$M_{w2}=\min\left\{\delta_{w2}\left[G-\eta(a-b\Gamma_w)\|\boldsymbol{w}(0)\|^2\right]\|\boldsymbol{w}(0)\|^2,\ \delta_{w2}\frac{4(\eta b\Gamma_w)^2G^3}{(\eta a+\eta b\Gamma_w)^3}\right\},$$

where \(G=1+\eta a\), \(a>b\Gamma_w\), and \(\delta_{w2}>0\) is a small constant. Clearly, \(M_{w2}>0\). Define two invariant sets as

$$\left\{\begin{aligned} S_{w1}&=\{w\mid w\in\mathbb{R}^n,M_{w1}\le\|w\|^2\le\frac{1+\eta a}{\eta a}\},\\ S_{w2}&=\{w\mid w\in\mathbb{R}^n,M_{w2}\le\|w\|^2\le\frac{1+\eta a}{\eta a+\eta b\Gamma_w}\}. \end{aligned}\right.$$

**Theorem 6.1** Suppose \(\eta>0\), \(a>0\), and \(b>0\). If \(\frac{b\Gamma_w}{a}<0.4074\) and \(\eta a<1\), then \(S_{w_1}\) is an invariant set of (6.1). If \(\frac{b\Gamma_w}{a}<0.2558\) and \(\eta a<1\), then \(S_{w_2}\) is an invariant set of (6.2).

*Proof.* From (6.1), it follows that

\[\mathbf{w}(k+1)=[1+\eta a-\eta a\|\mathbf{w}(k)\|^2]\mathbf{w}(k)+\eta b\Gamma_w\|\mathbf{w}(k)\|^2\|\mathbf{w}(k)\|\mathbf{w}(k),\]

for all \(k\geq 0\). Thus, there must exist \(\alpha(k)\) so that

\[\|\mathbf{w}(k+1)\|=\alpha(k)\left|1+\eta a-\eta a\|\mathbf{w}(k)\|^2\right|\|\mathbf{w}(k)\|+\eta b\Gamma_w\|\mathbf{w}(k)\|^2\|\mathbf{w}(k)\|,\]

for all \(k\geq 0\), where \(0<\alpha(k)\leq 1\). Since

\[\alpha(k)=\frac{\left|\left|1+\eta a-\eta a\|\mathbf{w}(k)\|^2\right|\mathbf{w}(k)+\eta b\Gamma_w\|\mathbf{w}(k)\|^2\|\mathbf{w}(k)\|\mathbf{w}(k)\right|}{\left|1+\eta a-\eta a\|\mathbf{w}(k)\|^2\right|\|\mathbf{w}(k)\|+\eta b\Gamma_w\|\mathbf{w}(k)\|^2\|\mathbf{w}(k)\|},\]

there must exist a small constant \(\delta_{w_1}\) so that \(0<\delta_{w_1}<\alpha(k)\leq 1\). So, if \(\|\mathbf{w}(k)\|^2\leq\frac{1+\eta a}{\eta a}\), it holds that

\[\|\mathbf{w}(k+1)\|^2=\left[\alpha(k)(1+\eta a)-\alpha(k)(\eta a-\eta b\Gamma_w)\|\mathbf{w}(k)\|^2\right]^2\|\mathbf{w}(k)\|^2,\]

for all \(k\geq 0\), where \(0<\delta_{w_1}<\alpha(k)\leq 1\). Since

\[\|\mathbf{w}(k)\|^2\leq\frac{1+\eta a}{\eta a}<\frac{\alpha(k)(1+\eta a)+1}{\alpha(k)(\eta a-\eta b\Gamma_w)},\]

where \(a>b\Gamma_w\), by Lemma 6.1, it follows that

\[\begin{aligned}\|\mathbf{w}(k+1)\|^2&=\left[\alpha(k)(1+\eta a)-\alpha(k)(\eta a-\eta b\Gamma_w)\|\mathbf{w}(k)\|^2\right]^2\|\mathbf{w}(k)\|^2 \tag{6.5}\\&\leq \max_{0<h<\psi(k)}\left\{\left[\alpha(k)(1+\eta a)-\alpha(k)(\eta a-\eta b\Gamma_w)h^2\right]^2h^2\right\}\\&\leq\frac{4[\alpha(k)(1+\eta a)]^3}{27\alpha(k)(\eta a-\eta b\Gamma_w)},\end{aligned}\]

where \(\psi(k)=\frac{1+\eta a}{\eta a-\eta b\Gamma_w}\). Clearly, if \(\frac{b\Gamma_w}{a}<0.4074\) and \(\eta a<1\), it follows that

\[\|\mathbf{w}(k+1)\|^2\leq\frac{4[\alpha(k)(1+\eta a)]^3}{27\alpha(k)(\eta a-\eta b\Gamma_w)}<\frac{1+\eta a}{\eta a}.\]

From (6.5), it follows that

\[\|\mathbf{w}(k+1)\|^2\geq\min_{0<h<\psi(k)}\left\{\left[\alpha(k)(1+\eta a)-\alpha(k)(\eta a-\eta b\Gamma_w)h^2\right]^2h^2\right\},\]
