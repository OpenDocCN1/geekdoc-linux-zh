![](bbox=[0.296, 0.08, 0.733, 0.313])

# **FIGURE 2.2**

A nonconvergent trajectory in $S(2)$.

Denote a unit hyper-sphere in $R^n$ by

$$U = \{w \mid w^T w \leq 1\}.$$

For any $w \in U$, it holds that

$$w^T Cw \leq \sigma w^T w \leq \sigma \leq \frac{1}{\eta},$$

i.e., $w \in S$. Thus, $U \subset S$. This suggests that one can select initial vector $w$ in $U-\{0\}$. From the application point view, choosing initial vectors from $U-\{0\}$ is an easy task. For example, we may simply generate an initial vector in $U$ by

$$w(0) = \frac{1}{\sqrt{n}} \cdot random(n).$$

# 2.3.4.3 Selection of Learning Rate

From the analysis in the last section, to guarantee convergence, the learning rate should satisfy $0 < \eta \leq 0.8899$. If we choose $\eta$ close to 0, from Lemma 2.2, it may slow down the convergence of $z_i(k)(j=m+1,\ldots,n)$. If we choose $\eta$ close to 0.8899, from Lemma 2.4, it may slow down the convergence of $z_i(k)(i=1,\ldots,m)$. To get a balance to suitably set $\eta$ for fast convergence, it would be better if

$$\theta_1 \approx \theta_2.$$

Under some mild conditions, it holds that

$$\theta_1 = \ln\left(\frac{1+\eta\sigma}{1+\eta\sigma_{m+1}}\right) \approx \ln(1+\eta\sigma),\quad \theta_2 \approx \ln\left(\frac{1}{\eta\sigma}\right).$$