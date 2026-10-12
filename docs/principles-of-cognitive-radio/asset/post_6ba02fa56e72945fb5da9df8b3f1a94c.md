
have been derived for a single-hop interweave network where multiple secondary users transmit in the presence of a single primary user in [92]. This work defined the notion of a *primary exclusive region*, or PER, around the primary transmitter. Secondary transmitters cannot operate within this PER, and the distance between a secondary user’s transmitter and receiver must be less than some specified distance. These two constraints restrict the amount of interference a secondary transmitter can cause to the primary receiver, and hence its outage probability, thereby enabling a closed-form derivation of scaling laws. The capacity was found to scale *linearly* with the number of secondary users, in contrast to the classical sublinear scaling in Gupta and Kumar’s result, where multihop routing was assumed. These interweave scaling law results were extended in [46] to a network with multiple primary as well as multiple secondary users, along with multihop routing. This work assumes that the locations of the primary user transmitters and receivers are known by the secondary network, and also that the primary network is less dense than the secondary network. The multipath routing protocols assume a *preservation region* around each primary node such that the secondary users route their traffic around these regions. If this routing protocol is shown to achieve almost the same scaling law as if the primary network was absent, while the primary network throughput is subject to only a fractional loss that decreases asymptotically. Specifically, a $K_{p\cdot r}$-user primary network achieves a throughput scaling of $\sqrt{K_{p}} = K_p^{0.5}$, while a $K_{s}$-user secondary network achieves a throughput scaling of $K_{s}^{0.5-\delta}$ for any $\delta > 0$ with arbitrarily small probability of outage. Similar scaling laws under the same model, constraints, and assumptions were obtained in [100], however in this work the location of the primary receivers was unknown. Hence preservation regions were only formed around the primary transmitters. This paper also showed that the same throughput-delay tradeoff as was obtained in [22] for a single asymptotically large network can be achieved by both the primary and secondary networks as the number of each type of user grows asymptotically. These results assume that the relative density of the primary users relative to the secondary users remains the same as the number of users grows.

## 2.7 **Overlay cognitive radio networks**

The motivation for overlay cognitive radio networks is to exploit intelligent radio capabilities to their fullest:
- from the information-theoretic point of view, the interweave constraint of orthogonal transmissions used by secondary and primary communicating pairs is unnecessarily restrictive and, as such, reduces capacity;
- cognitive capabilities can be exploited more broadly than just for spectrum hole detection.

For these reasons, and in contrast to interweave networks, overlay cognitive radio networks allow for concurrent secondary and primary transmissions over the same dimensions. Furthermore, in contrast to both interweave and underlay networks, in overlay networks a secondary transmitter may improve the communication of a primary user. In this setting, relaying and techniques for coping with interference become key tools to maximize the performance of both primary and secondary users.

### Modeling cognition
In the analysis of overlay cognitive radio models, the cognitive capability is typically captured by assuming that the secondary user’s encoder, called the *cognitive encoder*, knows the data sequence to be sent by the primary encoder in the next transmission block. This assumption is often too idealistic for practical systems. However, it is reasonable when the secondary and primary transmitters are close to each other, or the primary data sequence is being retransmitted after an initial failure and the secondary decoder was able to successfully decode it in the first transmission. This assumption is also applicable when the primary transmitter sends its data sequence in advance to a secondary transmitter, which might be done in a separate frequency band. Although idealistic, once the encoding and decoding strategies under this assumption are fully understood, this assumption can be relaxed to assume:
- that primary data sequences are conveyed to the secondary user over orthogonal links of finite capacities;
- that only partial data sequence knowledge is available, and this partial knowledge is used for partial decoding, or
- the primary data sequence is learned causally, to account for the time needed for decoding. These relaxations were investigated in [9, 58, 60].

### 2.7.1 Cognitive encoder for the two-user overlay channel

The simplest overlay cognitive network consists of one secondary and one primary pair, as shown in Fig. 2.17. The cognitive encoder corresponding to the secondary user is assumed to have full knowledge of data sequence $W_p$ communicated by the primary encoder to the primary decoder. The encoding strategies and channel gains are assumed known to all users in the channel. Overlay encoding techniques have mostly been investigated for this two-user channel. Without cognition, this network reduces to the two-user interference channel of Fig. 2.11 with the secondary user corresponding to user 1 and the primary user corresponding to user 2. Due to the similarities between these two models, in the information theory literature, this network is referred to as the *interference channel with one cognitive encoder*. It is also referred to as the cognitive radio channel, the interference channel with asymmetric message knowledge, the interference channel with degraded message sets, or the cognitive interference channel. Another special case of this channel model is obtained when the primary user does not transmit.

![](img/2d42983cf592ef4fc8a22646ddc49799_112_0.png)

Since the secondary transmitter knows the messages intended for both receivers, the channel reduces to the broadcast channel [16]. The two-user overlay channel thus contains elements of both interference and broadcast channels. The encoding strategies that have been developed for these canonical channels, or their combinations, are capacity-achieving for the overlay channel in certain conditions. We next review the encoding strategies that have been proposed for the two-user overlay channel, and discuss scenarios in which these schemes or their combinations achieve capacity.

Formally, the two-user overlay channel, with one secondary (cognitive) user and one primary user, consists of two input alphabets $\mathcal{X}_s$, $\mathcal{X}_p$, two output alphabets $\mathcal{Y}_s$, $\mathcal{Y}_p$, and a conditional probability distribution $p(y_s, y_p|x_s, x_p)$, where $(x_s, x_p) \in \mathcal{X}_s \times \mathcal{X}_p$ are channel inputs and $(y_s, y_p) \in \mathcal{Y}_s \times \mathcal{Y}_p$ are channel outputs. The secondary source wishes to send a message $W_s \in \mathcal{W}_s = \{1, \ldots, 2^{nR_s}\}$ to its destination, and the primary source wishes to send a message $W_p \in \mathcal{W}_p = \{1, \ldots, 2^{nR_p}\}$ to its destination. Data sequence $\hat{W}_p$ is also known at the secondary (cognitive) encoder. An $(R_s, R_p, n)$ code consists of two data sequence sets $\mathcal{W}_s$, $\mathcal{W}_p$, encoding functions

```
$$\begin{gathered}X_{s}^{n} = f_{s}\left(W_{s}, W_{p}\right), \
X_{p}^{n} = f_{p}\left(W_{p}\right), \end{gathered}\tag{2.64}$$
```

and two decoding functions

```
$$\hat{W}_{s} = g_{s}\left(Y_{s}^{n}\right), \hat{W}_{p} = g_{p}\left(Y_{p}^{n}\right). \tag{2.66}$$
```

The error probability of the code is

```
$$P_{e} = P\left[\left[\hat{W}_{s} \neq W_{s}\right]\bigcup\left[\hat{W}_{p} \neq W_{p}\right]\right]. \tag{2.67}$$
```

A rate pair $(R_s, R_p)$ is achievable if, for any $\epsilon > 0$, there exists, for sufficiently large $n$, an $(R_s, R_p, n)$ code such that $P_e \leq \epsilon$. The capacity region of the two-user overlay channel is the closure of the set of all achievable rate pairs $(R_s, R_p)$.

We observe that the only difference between this definition and the corresponding definitions for the interference channel is in the encoding function of the secondary cognitive encoder (2.64). Unlike in the interference channel, in this case the encoder knows both data sequences $W_s$ and $W_p$ and can thus form encoded sequences that depend on both of them. We will also consider the AWGN interference channel given by (2.33), augmented with cognitive encoding by the secondary user.

The additional information allows the cognitive encoder to deploy cooperation to increase the rate of the primary pair and precoding against interference to increase its own rate. Before summarizing encoding strategies used by the cognitive encoder, we give a brief overview of the Gelfand–Pinsker encoding technique. This technique, also referred to as *binning*, is used for the precoding against interference.

### Gelfand–Pinsker coding

For overlay networks, transmission by any primary transmitter causes interference at the secondary receiver. Since the cognitive encoder knows this interference, it deploys an encoding scheme that mitigates the effect of the interference at its receiver, thereby
