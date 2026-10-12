
across the entire signal level range. This potentially contaminates the adjacent channels with interference [42]. The PAPR of the signal in $x_n$, $n = 0, \dots, N-1$ in Eq. (1.1) is given by [84]

> $PAPR(\mathbf{x}) = \frac{\max_{0 \leq n \leq N-1} \{|x_n|^2\}}{\mathbb{E}\{|x_n|^2\}}$,

When the PAPR of the OFDM signal is large, the digital-to-analog converters and power amplifiers require high dynamic range to avoid clipping and distortion. Hence the dynamic range of digital-to-analog converters should be large enough to accommodate large peaks. One downside is that the cost of the digital-to-analog converters increases with higher dynamic range. In NC-OFDM systems, the PAPR will be larger since some of the subcarriers are nulled [75].

## 1.8 Spectrum coexistence in cognitive radio networks

One of the important requirements for the well-being of a cognitive radio network, for example in TV white spaces, is the healthy coexistence with the primary networks. There is a stringent requirement that secondary users should minimize the amount of interference at the primary receivers. Further, there is also the need for secondary users to be able to coexist and possibly form networks to carry information. There are many reactive methods that a cognitive radio could use to avoid interference. Typically, these involve adaptation of frequency, transmit power, and transmit waveforms. A frequency agile cognitive radio can periodically scan the entire band, identify if the channel is being used by the primary user and dynamically shift to another vacant band of the spectrum. Software defined radios can scan the spectrum either by sweeping the entire band or by frequency hopping and the RF hardware improvements have made such radios feasible. Power control is a widely used interference mitigation technique. With very minimal feedback based on the interference detected by periodic scanning, the transmit power of the secondary can be controlled to minimize the interference at the primary receiver. Orthogonalization of the signal space is another way of mitigating interference. In a time scheduling MAC of the secondary network, packets can be scheduled in time slots when primary user activity is not observed. Orthogonalizing in frequency is also a way to mitigate interference. NC-OFDM transmission discussed in the previous section is an example of orthogonalization in frequency domain. The above reactive mechanisms are limited by the amount of channel state information available at the transmitter and also due to the fact that interference is a receiver property. Reactive schemes inherently require explicit coordination protocols to obtain the network state and channel information of primary and secondary users. Without the network state information, efficient discovery, self-organization, resource management, and cooperation techniques are rendered inefficient. Exchanging link state information may overload the network and this poses a challenge for designing efficient networks using cognitive radios. This also emphasizes the need for the architecture and protocol mechanisms discussed earlier in Section 1.6.

### 1.8.1 Spectrum pooling and bandwidth exchange

The full power and benefits of cognitive radio technology can only be realized when cognitive radios form networks that can be used to carry information. Cooperative forwarding in wireless networks has been shown to yield rate and diversity gains, but it incurs energy costs borne by the cooperating nodes. Cognitive radio nodes have the ability to flexibly exchange the transmission bandwidth as a means of providing incentive for forwarding data, without increasing either the total bandwidth required or the total transmit power. The advent of multicarrier systems such as NC-OFDM with the ability to flexibly delegate and employ a number of subcarriers makes this approach particularly appealing compared to other incentive mechanisms that are often based on abstract notions of credit and shared understanding of worth.

*Spectrum pooling* is a concept where users may temporarily rent from a pool of spectral resources from primary users. The existing system of licensing spectrum need not be changed by this set-up. This system leads to a two-fold advantage: the secondary users get to access the spectral resources that they are not licensed to use, and the owners of the spectrum get to make revenue for the commodity they paid for but do not use extensively [89].

Among the many forms of cooperative communication, cooperative forwarding [12, 31] is an essential technique to enhance connectivity and throughput. As forwarding usually incurs bandwidth and energy cost, incentive mechanisms must be implemented to offset these. *Bandwidth exchange* (BE) [94], a concept similar to spectrum pooling, is an incentive mechanism that essentially enables a user to delegate a portion of its bandwidth in exchange for forwarding. Figure 1.11 illustrates the concept of BE in a network of nodes where a user incentivizes forwarding by delegating subcarriers to another user.

To motivate BE, consider Shannon's canonical channel capacity formula for an additive white Gaussian noise (AWGN) channel with a noise power spectral density of $N_{0}$.

![](img/2d42983cf592ef4fc8a22646ddc49799_53_0.png)

**Figure 1.11** When the direct link fails, user *i* tries to incentivize forwarding by delegating $N-N^{\min}$ subcarriers to user $j$ [93].

![](img/2d42983cf592ef4fc8a22646ddc49799_54_0.png)

$$C = W \log _{2}\left(1+\frac{\mathcal{P}}{N_{0} W}\right) \text { bits/second. }$$ (1.4)

In the above expression, $C$ is only logarithmically dependent on the average transmit power $\mathcal{P}$, but nearly linearly dependent on bandwidth $W$, especially when $W$ is relatively small. The largest partial derivatives with respect to these variables are given as

$$\left.\frac{\partial C}{\partial \mathcal{P}}\right|_{\mathcal{P}=0}=\frac{1}{N_{0} \log 2},\left.\frac{\partial C}{\partial W}\right|_{W=0}=\infty.$$ (1.5)

Equation (1.5) suggests that when power or bandwidth is constrained, the marginal utility achieved by using additional bandwidth is significantly greater. However, since the total bandwidth available in the network/system needs to be preserved, one may question whether it is really beneficial to reallocate bandwidth, since after all, when one node acquires additional bandwidth, it is at the expense of some other node(s) that loses an equal amount of bandwidth. Further, as the bandwidth increases (wide-node regime), the marginal increase in capacity saturates. Despite the marginal increase, a simple example can illustrate the performance gains from BE [94]. Consider the two-node network with an access point shown in Fig. 1.12. Suppose each node has a nonoverlapping bandwidth $(W_{1}=W_{2}=20 \mathrm{MHz})$ and fixed transmit power $(\mathcal{P}_{1}=\mathcal{P}_{2}=20 \mathrm{dBm})$. Also, for simplicity in illustration, suppose that the channels between the access point and the nodes as well as the channels between the nodes are determined by distance-based path loss, i.e., the rate achieved on a link is an explicit function of the bandwidth $W$ and channel power gain $G$, which is parametrized by its fixed transmit power $\mathcal{P}$. Let us assume this function is given by

$$C=C(W, G)=W \log _{2}\left(1+\frac{G \mathcal{P}}{N_{0} W}\right) \text { bits/second, }$$ (1.6)

where the channel gain $G=\kappa d^{-3}$ with $d$ being the distance and $\kappa$ being a proportionality constant that also captures the noise power spectral density $N_{0}$. For the geometry shown in Fig. 1.12, it follows that if both nodes only use direct links for transmission, node 1 achieves a transmission rate of $R_{1}^{\mathrm{dir}}=11 \mathrm{Mbps}$, while node 2 achieves

![](img/2d42983cf592ef4fc8a22646ddc49799_54_1.png)

**Figure 1.12** Bandwidth exchange enhances rates for both nodes simultaneously with $d_{1}=400 \mathrm{~m}, d_{2}=150 \mathrm{~m}, d_{12}=300 \mathrm{~m}, \kappa=6 \times 10^{4} \mathrm{MHz} \cdot \mathrm{m}^{3} / \mathrm{mW}$.
