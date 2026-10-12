
## 2.7 Overlay cognitive radio networks

![](img/2d42983cf592ef4fc8a22646ddc49799_114_0.png)

Figure 2.18 A channel with a random state. The state $S^n$ is known noncausally at the encoder.

increasing its rate. In the overlay channel, since the cognitive encoder has perfect knowledge of the data sequence and the encoding strategy of the primary user, the secondary transmitter–receiver pair can view this situation as communication in a channel with a random state noncausally known at the encoder, also known as the Gelfand–Pinsker problem [30], shown in Fig. 2.18. In this figure, a single source communicates a data sequence $W \in \{1, \ldots, 2^{nR}\}$ to the destination over a channel given by $p(y|x, s)$. The channel state sequence $S^n$ is assumed to be a random iid sequence generated from the distribution $p(s)$ over the random state. $S^n$ is noncausally known at the encoder.

We next consider an AWGN channel where the random state is an additional interference term $S$. Specifically, an AWGN channel with a random interference state has input–output relationship given by

$Y = X + S + Z, \tag{2.68}$

where $Z$ is zero-mean Gaussian noise at the receiver with power $\mathcal{N}$ and $S$ is zero-mean Gaussian noise at the receiver with power $\mathcal{N}_s$. The transmit power constraint is $\mathbb{E}[X^2] \le \mathcal{P}$. The Gelfand–Pinsker encoding in this channel model reduces to DPC, described above for the interference channel, whereby precoding is used to cancel the effect of the interference term $S$. In this setting DPC achieves the capacity of the AWGN channel as if there were no interference, i.e., it completely cancels the effect of interference $S$, yielding capacity

$C = W \log_2 \left( 1 + \frac{\mathcal{P}}{\mathcal{N}} \right) . \tag{2.69}$

The capacity of the general discrete-time memoryless channel with random state is given by

$C = \max_{p(u|x), f(.)} I(U;Y) - I(U;S), \tag{2.70}$

where $U \to (X, S) \to Y$ form a Markov chain, and is achieved by Gelfand–Pinsker encoding [30]. The random variable $U$ is used to generate a codebook at the encoder such that, in each block transmission, the codeword depends both on the data sequence and on the random state $S^n$. Gelfand–Pinsker encoding can play a crucial role in overlay cognitive radio, as will be described next.

Communication schemes deployed in the overlay channel contain the following three encoding strategies.

- 1 **Rate-splitting** Rate-splitting, as briefly described in Section 2.4, can improve rates for both communicating pairs by enabling (partial) interference cancellation at the decoders in the same fashion as in interference channels without cognition. This technique can potentially be deployed by both encoders, as it requires no cognition about other user’s data sequences as the encoder is only splitting its own rate. For the rate-splitting to be exploited by the primary user, this approach requires that the decoding at the primary receiver be modified to decode and cancel part of the secondary user’s transmission. This approach differs from the approach used in interweave and underlay cognitive radio where the communication technique of the primary users is not adapted in the presence of secondary users. If this constraint were to be imposed in overlay cognitive networks as well, the rate-splitting would be no longer applicable since it requires that the primary receiver decodes a part of the message of the secondary user.

- 2 **Cooperation** Full, partial, or delayed knowledge of the primary user’s data sequence allows the cognitive encoder to relay this information to the primary user, thereby increasing the rate of the primary pair. The cognitive encoder uses a fraction of its power to transmit message $W_p$ to the primary user and thus increases the primary rate $R_p$. When the primary user’s data sequence (or a part of it) is known to the cognitive encoder without the delay, i.e., at the beginning of the transmission block, relaying is performed via superposition coding, where secondary and primary messages are superimposed and sent by the cognitive encoder. Due to the noncausal knowledge, there is no need for Markov block encoding otherwise used for relaying [17].

- 3 **Gelfand–Pinsker encoding (binning)** Any signal carrying all or part of $W_p$ is interference at the secondary receiver. Hence, both the primary encoder and the cognitive encoder cause interference at the secondary receiver. However, if the cognitive encoder knows $W_p$ at the beginning of the transmission block (as well as the codecs and channel state information), it can infer the interference created at the secondary receiver. Knowing the interference, it can apply Gelfand–Pinsker encoding and, specifically in AWGN channels, DPC in order to precancel this interference. Another motivation for deploying Gelfand–Pinsker encoding is found in the relationship between the overlay channel and the broadcast channel whereby when the primary transmitter is silent, the overlay channel reduces to a two-user broadcast channel. For the discrete-time memoryless broadcast channel, the encoding scheme that yields the largest known achievable rate region is based on Gelfand–Pinsker encoding [61]. In the Gaussian case the two-user overlay channel is related also to the MIMO Gaussian broadcast channel. Specifically, a MIMO broadcast channel with two transmit antennas is equivalent to a two-user overlay channel when *both* encoders are cognitive, i.e., two encoders know the message intended for each receiver, since in fact these encoders are part of the same broadcasting transmission strategy. For MIMO Gaussian broadcast channels, DPC is the optimal encoding strategy [91, 94]. Motivated by these observations, binning and DPC have been applied to the two-user overlay channel, resulting in the highest known achievable rates, including capacity, in some cases, as will be presented later in this section.

### 2.7.2 Capacity results

Determining the capacity region for the general overlay channel remains an open problem. However, as for the interference channel without cognition, the capacity has been determined for some regimes. The capacity in strong interference has been determined in [60, Thm. 5]. The capacity for the Gaussian channel in weak interference has been derived in [49, 95]. For a more general case that unifies the results under these two regimes, the capacity was determined in [70]. For a class of discrete memoryless cognitive Z-channels (i.e., channels where there is no interference at the primary receiver) in which only the receiver of the secondary pair suffers interference the capacity has been determined in [56]. Capacity of a class of Gaussian cognitive Z-channels for the opposite case, when the interference is at the primary receiver, has been found in [47]. In each case, some combination of rate-splitting, cooperation, and/or binning achieves capacity. These regimes and their capacity-achieving encoding techniques are as follows.

### 1 Strong interference [60]

As in the interference channel, this is the regime in which both decoders can decode each other’s messages without rate penalty. In AWGN overlay channels, described by (2.33) with $X_1 = X_s$, $X_2 = X_p$, $h_{12} = h_{sp}$, $h_{21} = h_{ps}$ and the primary user’s message known at the secondary user’s transmitter, the following interference conditions are sufficient for strong interference to be satisfied:

$$
\begin{align*}
|h_{ps}| &\ge 1, \\
|h_{sp}| &\ge \frac{h_{ps}}{\alpha} + \frac{|\alpha - 1|}{\alpha} \quad \text{if } h_{sp} h_{ps} > 0, \\
|h_{sp}| &\ge \frac{h_{ps}}{\alpha} + \frac{\alpha + 1}{\alpha} \quad \text{if } h_{sp} h_{ps} < 0, \tag{2.71}
\end{align*}
$$

where $\alpha = \sqrt{P_s/P_p}$, for $P_s$ the received secondary transmit power at the secondary receiver and $P_p$ the received primary transmit power at the primary receiver. For $P_s = P_p$ and $h_{sp}, h_{ps} \ge 0$ these conditions simplify to

$$
h_{ps} \ge 1, h_{sp} \ge h_{ps}. \tag{2.72}
$$

In a general discrete-time memoryless channel, these conditions can be expressed in terms of the conditional mutual information as

$$
\begin{align*}
I(X_s; Y_s|X_p) &\le I(X_s; Y_p|X_p), \\
I(X_s, X_p; Y_s) &\le I(X_s, X_p; Y_p), \tag{2.73}
\end{align*}
$$

and need to be satisfied for all input distributions $p(x_s, x_p)$. We observe that the first inequality is the same condition as in the interference channel (2.35). In this regime, cooperation via superposition coding achieves capacity. The capacity region in an AWGN channel is
