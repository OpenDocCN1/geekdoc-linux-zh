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

# 4.5.1 Energy sensing

Consider the asymptotic performance of the energy detector, described by (4.25)–(4.26). Assume a Gaussian primary signal, $z(t)=w(t)$, and $w(t)$ Gaussian with zero mean and power known only in a certain interval. Eliminating $\theta$ from (4.25)–(4.26), we obtain

$$N = \left[ Q^{-1}(P_{\text{FA}}) - Q^{-1}(1 - P_{\text{MD}})(1 + \gamma) \right]^2 \gamma^{-2}.\tag{4.95}$$