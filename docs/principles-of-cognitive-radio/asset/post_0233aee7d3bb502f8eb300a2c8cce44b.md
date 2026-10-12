
## Known $\sigma_w^2$ and $\sigma_d^2$

We have, assuming $\tau$ unknown,$^1$

$p(\mathbf{y} \mid \mathcal{H}_0) = \frac{1}{\pi^N \sigma_w^{2N}} \exp\left(-\frac{\|\mathbf{y}\|^2}{\sigma_w^2}\right), \qquad (4.76)$

$p(\mathbf{y} \mid \mathcal{H}_1) = \frac{1}{\pi^N \det \mathbf{Q}_r^{-1}} \exp\left(-\mathbf{y}^\dagger \mathbf{Q}_r^{-1} \mathbf{y}\right), \qquad (4.77)$

where we have defined

$\mathbf{Q}_r \triangleq \sigma_d^2 \mathbf{T}_\tau \mathbf{T}_\tau^T + \sigma_w^2 \mathbf{I}, \qquad (4.78)$

Thus, the log-likelihood ratio for the decision between $\mathcal{H}_0$ and $\mathcal{H}_1$ has the form

$Y \triangleq \log \frac{p(\mathbf{y} \mid \mathcal{H}_1)}{p(\mathbf{y} \mid \mathcal{H}_0)} = \log \frac{\sigma_w^{2N}}{\det \mathbf{Q}_r} - \mathbf{y}^\dagger \left(\mathbf{Q}_r^{-1} - \sigma_w^{-2}\mathbf{I}\right) \mathbf{y}, \qquad (4.79)$

Direct computation of $\det \mathbf{Q}_r$ and of $\mathbf{y}^\dagger \left(\mathbf{Q}_r^{-1} - \sigma_w^{-2}\mathbf{I}\right) \mathbf{y}$ required to evaluate $Y$, may entail a considerable complexity when $N$ is large (see [1] for a simplification exploiting the sparseness of the matrix $\mathbf{Q}_r$).

As a special case, observe that with no cyclic prefix ($N_p = 0$, which corresponds to no usable structure of the observed signal), we have $\mathbf{T}_\tau, \mathbf{T}_\tau^T = \mathbf{I}$ and $\mathbf{y}|\mathcal{H}_1 \sim \mathcal{N}_c\left(0, (\sigma_d^2 + \sigma_w^2)\mathbf{I}\right)$, which results into the test statistic

$Y = \|\mathbf{y}\|^2$

and shows that the energy detector is optimal in these conditions.

## Unknown $\sigma_w^2$ and $\sigma_d^2$

If these two parameters are not known, but their a priori distribution is available, one may still use the likelihood-ratio test after eliminating them by standard marginalization:

$p(\mathbf{y} \mid \mathcal{H}_0) = \mathbb{E}_{\sigma_w^2} p(\mathbf{y} \mid \mathcal{H}_0, \sigma_w^2), \qquad (4.80)$

$p(\mathbf{y} \mid \mathcal{H}_1) = \mathbb{E}_{\sigma_w^2, \sigma_d^2} p(\mathbf{y} \mid \mathcal{H}_1, \sigma_w^2, \sigma_d^2), \qquad (4.81)$

which assumes the knowledge of the a priori distributions of $\sigma_w^2$ and $\sigma_d^2$. Another option is the use of the generalized likelihood ratio test (4.16), which consists here of replacing $\sigma_w^2$ and $\sigma_d^2$ with their maximum-likelihood estimates in (4.76)-(4.77).

## 4.4.2 Detection based on second-order statistics

The notation will be made simpler here if we redefine $N$ as $N = K(N_P + N_D) + N_D$. Now, consider the sample products

$$r_i \triangleq y_i^* y_{i+N_D}, \quad i = 0, \dots, K(N_P + N_D) - 1. \tag{4.82}$$

A key observation here is that, because of the repetition of data in the cyclic prefix, $y_i$ and $y_{i+N_D}$ may not be independent under $\mathcal{H}_1$, and hence the expected value of $r_i$ is nonzero even if $\mathbb{E} y_i = 0$. This property can be exploited for detection. Define the average sample value products

$$A_i \triangleq \frac{1}{K} \sum_{k=0}^{K-1} r_{i+k(N_P+N_D)}, \quad i = 0, \dots, N_P + N_D - 1. \tag{4.83}$$

Under hypothesis $\mathcal{H}_0$, all $A_i$ are identically distributed, while, under $\mathcal{H}_1$, $N_P$ samples $|A_i|$ will exhibit a different (and significantly larger for small noise) value than the remaining $N_D$. In fact, for $N_P$ consecutive indices $i$ we have $x_i = x_{i+N_D}$, while $x_i$ and $x_{i+N_D}$ are independent for the other $N_D$ indices. Thus, spectrum sensors can be designed which detect whether or not the $A_i$ are independent and identically distributed, or their statistics depend on $i$.

Defining the vector $\mathbf{A} \triangleq [A_0, \dots, A_{N_P+N_D-1}]^\mathrm{T}$, and using the generalized likelihood-ratio test (4.16), we obtain the test statistic

$$Y \triangleq \log \frac{\max_{\sigma_w^2,\sigma_z^2} p(\mathbf{A} \mid \mathcal{H}_1, \sigma_w^2, \sigma_z^2)}{\max_{\sigma_w^2} p(\mathbf{A} \mid \mathcal{H}_0, \sigma_w^2)}. \tag{4.84}$$

Details of the structure and the performance of these sensors are described in [1].

Other spectrum sensors, based on second-order statistics of OFDM signals, have also been advocated. Hereafter, we describe some of them (a quantitative comparison of their performance is contained in [1]).

### Autocorrelation detector

The test statistic proposed in [4] consists of the empirical mean of the products $r_i$, normalized by the received power:

$$Y \triangleq \frac{\sum_{i=0}^{(N_P+N_D)-1} \overline{A_i}}{N^{-1}(N_P+N_D) \sum_{i=0}^{N-1} |y_i|^2}, \tag{4.85}$$

where $\overline{A_i} \triangleq \Re\{A_i\}$. This detector does not need the value of the noise variance $\sigma_z^2$. On the other hand, it does not exploit the fact that, under $\mathcal{H}_1$, the observed signal is nonstationary.

### Cyclic-prefix detector

The test statistic of this detector is [27]

$Y \triangleq \left| \frac{1}{N} \sum_{i=0}^{(N_P+N_D)-1} A_i + c \right|^2, \quad (4.86)$

where

$c \triangleq \frac{\frac{N_P}{N_P+N_D}\sigma_z^2}{\left(1+2\left(\frac{N_P}{N_P+N_D}\right)^2\right)\frac{\sigma_d^2}{\sigma_z^2}+2}, \quad (4.87)$

Even this detector does not exploit the nonstationarity of the observed signal. Notice how the calculation of this test statistic requires the knowledge of $\sigma_d^2$ and $\sigma_z^2$. To remove this requirement, one may choose to set $c = 0$. However, the decision threshold would still depend on the noise variance $\sigma_z^2$.

### Sliding-window detector

This detector [21] uses a sliding window summing $r_i$ over $N_P$ consecutive samples and taking the maximum. The test statistic is

$Y \triangleq \left| \sum_{i=\tau}^{\tau+N_P-1} r_i \right|, \quad (4.88)$

A simple extension of this detector [1] is obtained by taking $K$ OFDM symbols instead of one:

$Y \triangleq \left| \sum_{i=\tau}^{\tau+N_P-1} A_i \right|, \quad (4.89)$

Setting the decision threshold of this detector requires knowledge of the value of $\sigma_z^2$.

## 4.5 Effects of imperfect knowledge of noise power

The calculations presented before in this chapter can be used to compare the performance of various detectors based on their receiver operating characteristics (ROCs), which in turn are highly dependent on the SNR and on the sensing time $N$. Increasing the latter yields a performance improvement, but only under the optimistic assumption that the model used in the analysis is infinitely accurate. Since this assumption can not hold in the real world (for example, noise is never perfectly Gaussian, or white, or wide-sense stationary), it happens, as shown in this section, that model uncertainties may impose fundamental limitations on the performance of the detectors, as we shall discuss soon, by a lack of robustness in the detector. In this section and the next we shall examine how imperfect channel modeling can affect spectrum sensing.

Consider again the sampled-signal observation

$$y_n = h x_n + z_n,\tag{4.90}$$

where $x_n$ is the primary signal, affected by block fading $h$, and $z_n$ is additive disturbance. As usual, the primary signal is assumed to be independent of both noise and fading. Now, derivations based on (4.90) must assume that $(y_n)$, $h$, $(x_n)$, and $(z_n)$ are modeled with infinite precision, which requires, for example, that receiver nonlinearities, quantization noise, and interferences from other signal sources can be disregarded as irrelevant. A more realistic view of the problem would require, for example, that the noise process $(z_n)$ be modeled as having a distribution Z taken from a set of possible distributions $\mathcal{Z}$, which we may call the *noise uncertainty set*. A similar approach would be followed for the other entities in (4.90), modeled as having distributions H and X taken from suitable uncertainty sets H and X.

A detector whose decision strategy is $\mathcal{D}_N$ is said to be *robust* for target probabilities $P_{\text{FA}}$ and $P_{\text{MD}}$ if

$$\sup_{Z \in \mathcal{Z}} P_{\text{FA}}(Z) \le P_{\text{FA}},\tag{4.91}$$

$$\sup_{H \in \mathcal{H}, X \in \mathcal{X}, Z \in \mathcal{Z}} P_{\text{FA}}(H,X,Z) \le P_{\text{MD}}.\tag{4.92}$$

Conversely, the detector is said to be *nonrobust* at a certain SNR if, even when $N$ is made arbitrarily large, there are pairs $(P_{\text{FA}}, P_{\text{MD}})$, $0 < P_{\text{FA}} < 1/2$ and $0 < P_{\text{MD}} < 1/2$, that cannot be achieved. Mathematically, a detector is robust if and only if the sets of means of $Y$ under both hypotheses do not overlap, i.e., $A_N \cap B_N = \varnothing$, where

$$A_N \triangleq \{ \mathbb{E}_2[Y \mid \mathcal{H}_0] : Z \in \mathcal{Z} \},\tag{4.93}$$

$$B_N \triangleq \{ \mathbb{E}_2[Y \mid \mathcal{H}_1] : H \in \mathcal{H}, X \in \mathcal{X}, Z \in \mathcal{Z} \},\tag{4.94}$$

and $\mathcal{X}$ includes signal distributions with the same average power $\mathcal{P}$. It turns out that robustness is easier to achieve if the SNR is high. In this situation the distributions of the test statistics under both hypotheses are sufficiently separated, and modeling uncertainties may not mix them. At low SNR, the sets of distributions of $Y$ under both hypotheses may completely overlap. If an SNR threshold $\gamma_t$ exists such that the detector becomes nonrobust for all SNRs lower than $\gamma_t$, then such a $\gamma_t$ is called the *SNR wall* for the detector. The SNR wall quantifies the degree of robustness of the detector. In the balance of this section we examine three examples of SNR walls. For a more comprehensive discussion, the reader is referred to [39–42].

### 4.5.1 Energy sensing

Consider the asymptotic performance of the energy detector, described by (4.25)–(4.26). Assume a Gaussian primary signal, $z(t)=w(t)$, and $w(t)$ Gaussian with zero mean and power known only in a certain interval. Eliminating $\theta$ from (4.25)–(4.26), we obtain

$$N = \left[ Q^{-1}(P_{\text{FA}}) - Q^{-1}(1 - P_{\text{MD}})(1 + \gamma) \right]^2 \gamma^{-2}.\tag{4.95}$$
