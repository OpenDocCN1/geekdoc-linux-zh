
$R \leq \max_{p\{x_s, x_r\}} \min\{I(X_s; Y_r | X_d), I(X_s, X_d; Y_r)\}$. (2.25)

In the AWGN relay channel this yields

$R \leq \max_{0 \leq \rho \leq 1} \min\{W \log_2 (1+P_s+P_r+2\rho\sqrt{P_s P_r}), W \log_2 (1+(P_s+P_r)(1-\rho^2))\}$, (2.26)

where we normalize the noise power to one. The parameter $\rho$ determines the coherent combining gain of source and relay inputs $X_s$ and $X_r$ at the destination. A larger $\rho$ corresponds to a larger gain.

The cut-set bound is a tight outer bound only for certain special scenarios. In general, the cut-set bound is looser relative to the network capacity region. Alternative outer bounds to the cut-set outer bound can be derived by using *genie*-based techniques in which the network is modified by assuming that additional information is known (a.k.a., given by a genie) to a subset of terminals. The goal of providing this information is to obtain a modified network for which capacity or an outer bound can be obtained. Due to the additional information, the modified network outperforms the original one. Consequently, its capacity (or any outer bound on it) yields a capacity outer bound for the original network. Outer bounds can also be obtained by *the theory of network equivalence* [50]. This approach provides conditions under which the capacity of a wireless network can be upper bounded by the performance of an equivalent noiseless network of bit pipes, for which the capacity can then be determined. Another technique to tighten the cut-set bound is by modification of the network connectivity graph [52, 53].

Obtaining the Shannon capacity region of a wireless network is generally intractable; in fact the capacity of several simple canonical topologies such as the relay channel and the interference channel have remained open problems for decades. As an alternative capacity metric, a landmark result by Gupta and Kumar [38] introduced the notion of scaling laws for noncongestive wireless network throughput as the number of nodes in the network $K$ grows asymptotically large. They found that the throughput in terms of bits per second for each node in the network decreases with $K$ at a rate between $1/\sqrt{K\log K}$ and $1/\sqrt{K}$. In other words the per-node rate of the network goes to zero, although the total network throughput, equal to the sum of rates, grows at a rate between $\sqrt{K/\log K}$ and $\sqrt{K}$. This surprising result indicates that even when interference is treated as noise (as is typical in practical designs), even with optimal routing and scheduling, the per-node rate in a large ad hoc wireless network goes to zero. The reason is that in this relatively simple relaying scheme, intermediate nodes spend much of their resources forwarding packets for other nodes, so few resources are left to send down data. There has been much follow-on work to this result, including the impact on wireless network scaling laws of mobility, multiple antennas, and cooperation [5, 36, 68]. In particular, [68] showed that more sophisticated cooperation schemes allow per-node rates in large networks to remain constant with network size rather than decrease. The tradeoff between throughput (in terms of scaling laws) and delay in asymptotically large networks was characterized in [22, 39, 85].

## 2.4 Interference channels without cognition

### 2.4.1 K-user interference channels

In cognitive radio networks, we would like to characterize capacity associated with communications between primary user pairs and between secondary user pairs. Although one could envision deployment of relays to improve the performance, these networks typically do not involve multipath routing of information, i.e., there is no forwarding of information through intermediate nodes. Without cognition, networks with K source-destination pairs can be modeled as a K-user interference channel, as shown in Fig. 2.10. Although the capacity region of this channel is in general unknown, there has been a lot of progress in understanding how to cope with interference in this model and, consequently, in developing spectrally-efficient transmission schemes for this channel. In some scenarios, these techniques lead to capacity. A cognitive radio network forms a two-tier K-user interference channel, due to the different capabilities and restrictions of primary and secondary users. Schemes that efficiently cope with interference can improve performance of both primary and secondary users in these networks. For that reason, some of the techniques developed for interference channels have been adopted for overlay cognitive networks as well. We next review these techniques, their performance and their known capacity results. In addition, cognition enables additional encoding/decoding techniques to improve the performance. Hence, performance of interference channels can serve as a lower bound to the capacity of cognitive networks.

In the K-user interference channel model, each of the K sources wishes to communicate with its corresponding destination over a shared wireless channel, as illustrated in Fig. 2.10. Source s_k encodes and sends a data sequence W_k at rate R_k to destination d_k. The K-user interference channel is a special case of a K-user wireless network, and hence we use the same definitions as in Section 2.3.1 for encoding, decoding, error probability, and capacity. However, the encoding function of the kth user in the interference channel is given by

![](img/2d42983cf592ef4fc8a22646ddc49799_90_0.png)

$X_{k}^{n}=f_{k}\left(W_{k}\right)$. (2.27)

Thus, in this case a channel input at each source depends only on its own data sequence, which, in turn, is independent of data sequences from other sources. Hence, there is no cooperation (e.g., relaying) between sources in transmitting information about each other's data sequences. The cut-set bound (2.21) can then be tightened to become

$\sum_{s_{k}\in\mathcal{S}_{n},\ d_{k}\in\mathcal{S}_{n}^{c}} R_{k}\leq I\left(X(\mathcal{S}_{n});Y(\bar{\mathcal{S}_{n}})|X(\mathcal{S}_{n}^{c}),V\right)$ (2.28)

for any $p(v)\prod_{k} p(x_{k}|v)$, where $V$, referred to as a *time-sharing random variable*, has the property that the inputs $\{x_{k}\}$ are independent when conditioned on $V$.

Lower bounds to the capacity region are obtained by deploying specific communication techniques in the given network. We next present encoding schemes that achieve capacity for special cases of the two-user interference channel.

### 2.4.2 Two-user interference channel capacity

A two-user discrete-time memoryless interference channel is shown in Fig. 2.11. The interference channel contains only two communicating pairs ($K=2$). Therefore, there are two channel inputs, $X_1$ and $X_2$, and two channel outputs, $Y_1$ and $Y_2$. The discrete-time channel is characterized by the conditional distribution $p(y_1,y_2|x_1,x_2)$. Each source $s_k$, $k=1,2$, wishes to send a data sequence $W_k \in \mathcal{W}=\{1,\dots,2^{nR_k}\}$ to destination $d_k$. Definitions for the channel code, the error probability and the capacity region follow the definitions for the $K$-user interference channel. In particular, an $(R_1,R_2,n)$ code consists of two data sequence sets $\mathcal{W}_1,\mathcal{W}_2$, two encoding functions

$X_{1}^{n}=f_{1}\left(W_{1}\right)$. (2.29)
$X_{2}^{n}=f_{2}\left(W_{2}\right)$ (2.30)

and two decoding functions
$\hat{W}_{k}=g_{k}\left(Y_{k}^{n}\right), \quad k=1,2$. (2.31)

![](img/2d42983cf592ef4fc8a22646ddc49799_91_0.png)

The error probability of the code is

$$P_{\mathrm{e}}=P\left[\left[\hat{W}_{1} \neq W_{1}\right] \cup\left[\hat{W}_{2} \neq W_{2}\right]\right].$$

A rate pair $(R_{1}, R_{2})$ is achievable if, for any $\epsilon>0$, there exists for sufficiently large $n$ an $(R_{1}, R_{2}, n)$ code such that $P_{\mathrm{e}} \leq \epsilon$. The capacity region of the interference channel is the closure of the set of all achievable rate pairs $(R_{1}, R_{2})$.

We will also consider the two-user AWGN interference channel, defined by

$$\begin{array}{l}Y_{1}=X_{1}+h_{12} X_{2}+Z_{1}, \\ Y_{2}=h_{21} X_{1}+X_{2}+Z_{2},\end{array}$$

where $h_{12}$ and $h_{21}$ are the (real) cross-channel gains of the interfering links, $\mathbb{E}\left[X_{k}^{2}\right] \leq \mathcal{P}_{k}$ are power constraints, and $Z_{k} \sim \mathcal{N}(0,1)$ for $k=1,2$, where $\mathcal{N}(0, \sigma^{2})$ denotes the Gaussian distribution with variance $\sigma^{2}$.

The capacity of the interference channel is known in the case of $strong$ interference $[15]$. In this regime, the interfering signal at each receiver is strong enough that the other user's data sequence carried by that signal can be decoded and hence removed. It is then optimal for each receiver to decode both data sequences. In the AWGN interference channel (2.33), the strong interference conditions are given by $[40,74]$

$$\begin{array}{l}\left|h_{12}\right| \geq 1, \\ \left|h_{21}\right| \geq 1,\end{array}$$

implying that in this regime the cross-channel gains are larger than the direct link gains.

In general discrete memoryless channels, the strong interference conditions can be expressed in terms of the conditional mutual information inequalities. These conditions require that

$$\begin{array}{l}I\left(X_{1} ; Y_{1} \mid X_{2}\right) \leq I\left(X_{1} ; Y_{2} \mid X_{2}\right), \\ I\left(X_{2} ; Y_{2} \mid X_{1}\right) \leq I\left(X_{2} ; Y_{1} \mid X_{1}\right)\end{array}$$

are satisfied for every distribution $p\left(x_{1}\right) p\left(x_{2}\right)$. From (2.35) we observe that $Y_{2}$ contains more information about input $X_{1}$ than $Y_{1}$, given $X_{2}$. Hence, $X_{1}$ conveys more information to receiver 2 than to receiver 1. A similar interpretation can be made for (2.36).

The capacity region in strong interference is given by

$$\begin{gathered}\mathcal{C}=\bigcup\left\{\left(R_{1}, R_{2}\right): R_{1} \geq 0, R_{2} \geq 0,\right. \\\left.\begin{array}{l}R_{1} \leq I\left(X_{1} ; Y_{1} \mid X_{2}, V\right), \\ R_{2} \leq I\left(X_{2} ; Y_{2} \mid X_{1}, V\right), \\ R_{1}+R_{2} \leq \min \left\{I\left(X_{1}, X_{2} ; Y_{1} \mid V\right), I\left(X_{1}, X_{2} ; Y_{2} \mid V\right)\right\}\end{array}\right\}\end{gathered}$$

where the union is over distributions of the form $p(v) p\left(x_{1}|v\right) p\left(x_{2}|v\right)$ and $V$ is once again a time-sharing random variable for which the inputs are independent when conditioned on it.
