
$$\mathcal{C}=\bigcup_{|\rho|\leq1}\left\{\left(R_{s}, R_{p}\right): R_{s}\geq0, R_{p}\geq0,$
$R_{s}\leq\frac{1}{2}\log\left(1+\left(1-\rho^{2}\right)P_{s}\right),$ (2.74)
$R_{s}+R_{p}\leq\frac{1}{2}\log\left(1+P_{s}+P_{p}+h_{\mathrm{ps}}^{2}P_{s}+2\rho h_{\mathrm{ps}}\sqrt{P_{s}P_{p}}\right)\right\},$ (2.75)

where $\rho$ is the correlation between inputs $X_{s}$ and $X_{p}$. Note that a larger $\rho$ results in a larger coherent combining gain at the primary receiver of the secondary and primary transmissions of the primary user’s data. The general capacity region is

$$\mathcal{C}=\bigcup\left\{\left(R_{s}, R_{p}\right): R_{s}\geq0, R_{p}\geq0,$
$R_{s}\leq I\left(X_{s};Y_{s}|X_{p}\right),$ (2.76)
$R_{s}+R_{p}\leq I\left(X_{s},X_{p};Y_{p}\right)\right\},$ (2.77)

where the union is over all input distributions $p(x_{s},x_{p})$.

## 2 Weak interference at the primary receiver [49, 95]

In the AWGN overlay channel (2.33), weak interference at the primary receiver corresponds to $\left|h_{\mathrm{ps}}\right|\leq1$, i.e., the cross-channel gain from the secondary to the primary user is smaller than the direct link gain. Because the interference is weak, the primary receiver does not attempt to decode the unwanted data sequence and instead treats it as noise. Interference at the secondary receiver can be eliminated by DPC at the cognitive encoder, allowing for the interference-free, single-user rate to be achieved.

The optimum coding strategy at the cognitive encoder consists of encoding message $W_{s}$ via DPC while treating the primary user’s input sequence $X_{p}^{n}$ as interference, and superposition coding to help convey $W_{p}$ to the primary receiver. Thus, there is no need for rate-splitting; DPC and cooperation via superposition coding achieve capacity. The capacity region is

$$\begin{array}{r} { R_{s}\leq\frac{1}{2}\log(1+\alpha P_{s})},\\ { R_{p}\leq\frac{1}{2}\log\left(1+\frac{\left(h_{\mathrm{ps}}\sqrt{\alpha P_{s}}+\sqrt{\overline{P_{p}}}\right)^{2}}{1+h_{\mathrm{ps}}^{2}\left(1-\alpha\right)P_{s}}\right)}, \end{array}$$
(2.78)
(2.79)

where $\alpha$ is the fraction of power that the cognitive encoder uses for cooperation. The rest of the power, $(1-\alpha)P_{s}$, the cognitive encoder uses to transmit the signal carrying its own data. That signal is the interference at the primary receiver.

In the case of the discrete-time memoryless channel, the weak interference conditions are given by:

$$\begin{array}{c} I\left(U;Y_{p}|X_{p}\right)\leq I\left(U;Y_{s}|X_{p}\right),\\ I\left(X_{p};Y_{s}\right)\leq I\left(X_{p};Y_{p}\right) \end{array}$$ (2.80)

for all distributions $p(u,x_{s},x_{p})$. The random variable $U$ has the same role as in the Gelfand-Pinsker encoding, i.e., it is used for precanceling the interference via binning. The capacity region is

## 2.7 Overlay cognitive radio networks 91

![](img/2d42983cf592ef4fc8a22646ddc49799_118_0.png)

$$\begin{aligned} & \mathcal{C}=\bigcup \left\{\begin{array}{l} \left(R_{s}, R_{p}\right): R_{s} \geq 0, R_{p} \geq 0, \\ R_{s} \leq I\left(X_{s} ; Y_{s}| U, X_{p}\right), \\ R_{p} \leq I\left(U, X_{p}; Y_{p}\right) \end{array}\right\}, \end{aligned}$$
where the union is over all distributions $p(u, x_{s}, x_{p})$.
Regimes of strong and weak interference for Gaussian channels with $\mathcal{P}_{s}=\mathcal{P}_{p}$ for $h_{sp}, h_{ps} \geq 0$ are shown in Fig. 2.19.

### 3 Better cognitive decoding regime [70]

This is the regime for which the condition
$$I\left(U, X_{p} ; Y_{p}\right) \leq I\left(U, X_{p} ; Y_{s}\right)$$
holds for any $p(u, x_{s}, x_{p})$.
The capacity region is given by
$$\begin{gathered} R_{s} \leq I(U, X_{s} ; Y_{s}| X_{p}), \\ R_{p} \leq I(U, X_{p} ; Y_{p}), \\ R_{s}+R_{p} \leq I(U, X_{p} ; Y_{p})+I\left(X_{s} ; Y_{s}| X_{p}, U\right), \\ R_{s}+R_{p} \leq I\left(U, X_{s}, X_{p} ; Y_{s}\right). \end{gathered}$$
Again, the random variable $U$ has the same role as in the Gelfand–Pinsker encoding, i.e., it is used for binning. In addition to binning and superposition coding, the encoding scheme requires rate-splitting at the cognitive encoder.

### 4 Common information

If the cognitive decoder wishes to decode both data sequences, there is no interference at that decoder and hence there is no need for binning. Then, rate-splitting and superposition coding achieve capacity [48, 55].

The capacity results presented above indicate that in order to maximize performance of cognitive radio networks, its users should be allowed to share the bandwidth and cope with the introduced interference via (partial) decoding, relaying or precoding. Gains from the various techniques depend on channel conditions and the network topology.

As explained earlier, gains also depend on the amount of information that the cognitive radio is able to collect about the primary user transmissions.

For overlay channels, results that incorporate time variations in the channel model are scarce. One possible approach to model time variations is to assume that channel parameters depend on the random state sequence. In a point-to-point channel when the encoder knows the random state, this approach leads to the Gel'fand-Pinsker problem discussed earlier in this section. Overlay channels with a state were analyzed in [82]. This model generalizes the overlay channel that assumes constant channel gains. The paper develops inner and outer bounds for overlay channels with a state, and establishes capacity in the weak interference regime.

Another important aspect of the overlay channel capacity is the impact of imperfect channel state information (CSI) at the cognitive encoder. The lack of channel knowledge will affect all cognitive encoding schemes. With phase uncertainty at the cognitive encoder, DPC cannot be applied directly. Hence this uncertainty precludes canceling interference and results in significant performance loss [37]. In this case, feedback about channel state information to the cognitive encoders could be very beneficial. Relaying strategies can be realized without CSI at the transmitter, but would require CSI at the receiver [51]. However, CSI at the transmitter could allow for additional relaying approaches (e.g., beamforming) and thus further improve the network performance.

### 2.7.3 K-user overlay networks

Analysis of the two-user overlay channel focuses on a single secondary pair and a single primary pair. Yet, as in the interweave networks, multiple secondary and multiple primary users in the overlay network can simultaneously share the same spectrum. As with the two-user overlay case, in this more general setting we also seek efficient ways to minimize interference among users.

We have seen in Section 2.4 that for the K-user interference channel, generalizing the rate-splitting approach as a way to cope with interference from multiple senders is too complex. Moreover, this approach can be outperformed by collective treatment of interference via interference alignment or structured codes. Not surprisingly, interference alignment as well as structured codes are promising approaches for the K-user overlay cognitive radio network as well. These techniques could be deployed by cognitive nodes to reduce the interference at both the primary and the cognitive receivers. But in contrast to the encoders in interference channels, secondary users can also perform relaying of primary messages, and precoding against interference. The interplay between these techniques is not yet well understood and presents an important and interesting research topic.

Another interesting problem is the impact of cognition when present at different points in the network. In particular, not only encoders but also (or only) decoders can be cognitive. This will significantly impact the available encoding and decoding techniques. No cognition at the encoder will preclude both cooperation and precoding techniques. On the other hand, it will enable decoders to directly cancel interference. The
