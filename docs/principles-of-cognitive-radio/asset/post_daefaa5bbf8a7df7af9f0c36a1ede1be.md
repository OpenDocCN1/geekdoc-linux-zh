
for some “cutoff” value $\gamma_0$ which is found via the average power constraint. If $\gamma(t)$ is below this cutoff at time *t* then no data are transmitted at that time. With this optimal power allocation, the capacity of the time-varying flat-fading channel becomes

$$C = \int_{\gamma_0}^{\infty} W \log_2 \left( \frac{\gamma}{\gamma_0} \right) p(\gamma)d\gamma, \qquad\qquad\qquad\qquad\qquad(2.17)$$

where the rate corresponding to instantaneous SNR $\gamma$ is $W \log_2(\gamma/\gamma_0)$. Since $\gamma_0$ is constant, this means that as the instantaneous SNR increases, the data rate sent over the channel for that instantaneous SNR also increases.

There is a strong similarity between time-varying flat-fading channels, MIMO channels, and time-invariant frequency-selective fading channels in that these channels can be represented as a set of independent parallel channels in time, space, or frequency, respectively. This property can be exploited in cognitive radio paradigms, in particular the interweave paradigm. Specifically, if the cognitive radio can sense that a given dimension in time, space, or frequency is not being utilized by the primary user, it can occupy that dimension with no harm to the primary system. The capacity analysis for interweave systems is based on this concept, whereby the interweave cognitive radio channel is modeled as a channel varying over time, frequency, or space. When a given dimension is occupied by the primary user, under perfect sensing the interweave channel in that dimension is unavailable to the cognitive radio, i.e., it is assumed to have an SNR of zero. The capacity analysis above for parallel channels in time, space, or frequency can then be applied directly to determine the capacity of the interweave cognitive radio, as described in more detail in Section 2.6.

The capacities of multiuser channels and wireless networks are also built upon notions of mutual information. However, the encoding and decoding strategies and their associated mutual information become more complicated with multiple users, and hence the capacity regions are typically defined by a set of mutual information bounds that implicitly define the capacity region boundary. Before launching into capacity results for the different cognitive radio paradigms, we will first review capacity results for the interference channel. Since, as discussed in Section 2.3.1, cognitive radio networks are generalizations of the interference channel in Fig. 2.7, the capacity region and optimal encoding and decoding strategies of the interference channel will provide fundamental building blocks for obtaining capacity and design insights for cognitive networks.

### 2.3.3 Capacity region of wireless networks
We consider a wireless network consisting of $K$ source-destination pairs communicating over a common wireless channel, as shown in Fig. 2.9. We assume a discrete-time network model with discrete channel inputs and outputs. At each time instant, a source $s_k$ chooses a channel input $X_k$ from a finite set $\mathcal{X}_k$ of possible inputs. Each destination node $d_j$ observes a channel output $Y_j$ from output set $\mathcal{Y}_j$. The channel is described by the conditional distribution $p(y_1, \dots, y_K | x_1, \dots, x_K)$, which characterizes the probability of the given set of outputs $(y_1, \dots, y_K)$ at the destinations, for the given set of channel inputs $(x_1, \dots, x_K)$. A source $s_k$ wishes to communicate a data sequence or
![](img/2d42983cf592ef4fc8a22646ddc49799_87_0.png)
Figure 2.9 Wireless network model.
message $W_{k}\in\mathcal{W}_{k} = \{1, \dots, 2^{nR_{k}}\}$ to destination $d_{k}$, at rate $R_{k}$. To do so, the source encoder maps the data sequence into a codeword $X_{k}^{n}$ consisting of $n$ symbols from the input alphabet, and sends it in $n$ time instants over the channel. All data sequences are mutually independent. Upon receiving the sequence $Y_{j}^{n}$ of length $n$, decoder $j$ maps it to its estimate of the transmitted data sequence, denoted by $\hat{W}_{j}$. The data sequence sets $\mathcal{W}_{1}, \mathcal{W}_{2}, \dots, \mathcal{W}_{K}$ along with the encoder and decoder mappings of all users define an $(R_{1}, R_{2}, \dots, R_{K}, n)$ code for this channel. The encoding function at source $s_{k}$ for data sequence $W_{k}$ at time $i$ is given by

$X_{k,i} = \mathit{f}_{k,i}(W_{k}, Y_{k}^{i-1}), \quad\quad k = 1, \dots, K. \tag{2.18}$

Note that the encoding function $\mathit{f}_{k,i}(\cdot)$ allows the source to use its receiver’s previous observations of the channel (typically obtained via feedback) to encode $W_{k}$. This allows sources to obtain information about data sequences sent by other users and potentially forward them through the network. The decoding function at destination $j$ at time $i$ is given by

$\hat{W}_{j} = g_{j}(Y_{j}^{n}), \quad\quad j = 1, \dots, K. \tag{2.19}$

A decoding error at destination $k$ occurs when $\hat{W}_{k} \neq W_{k}$. We consider that an error occurs unless all destinations decode their data sequences correctly. Thus, the error probability is given by the probability of the union of error events associated with incorrect detection on each of the different data sequences:

$P_{e} = P \left[\bigcup_{k=1}^{K} \left[\hat{W}_{k} \neq W_{k}\right]\right]. \tag{2.20}$

If the error probability can be made arbitrarily small for a code of sufficiently large $n$, the rates $(R_{1}, \dots, R_{K})$ will be simultaneously achievable in the considered network. More precisely, rates $(R_{1}, R_{2}, \dots, R_{K})$ are achievable if, for any $\epsilon > 0$, there exists, for sufficiently large $n$, an $(R_{1}, R_{2}, \dots, R_{K}, n)$ code such that $P_{e} \leq \epsilon$. The capacity region is the closure of the set of all achievable rates $(R_{1}, \dots, R_{K})$, due to time-sharing between strategies associated with any set of points on the rate region.

## 2.3 Fundamental performance limits 61
The above formulation assumes a single destination for each data sequence. This definition can be extended to include multicasting to a set of destinations, broadcasting from one source to a set of destinations or multiple access from multiple sources to a single destination. The capacity region of a general wireless network is unknown. A general outer bound on the network performance is provided by the cut-set bound [2, 18, 23, 78], stated next.

Let $\mathcal{S}$ denote a subset of all network nodes and $\mathcal{S}^c$ be the complement of $\mathcal{S}$. The pair $(\mathcal{S}, \mathcal{S}^c)$ is a *cut* separating source $s_k$ and destination $d_k$ if source $s_k \in \mathcal{S}$ and $d_k \in \mathcal{S}^c$.

### Cut-set outer bound
Any achievable $(R_1,\dots,R_K)$ satisfies

$$\sum_{s_k \in \mathcal{S}, d_k \in \mathcal{S}^c} R_k \leq I(X(\mathcal{S}); Y(\mathcal{S}^c) | X(\mathcal{S}^c)),$$ (2.21)

where mutual information is evaluated for some distribution $p(x_1,\dots,x_K)$ for any $\mathcal{S}$. $R_k$ is the rate across the cut from source $s_k$ to destination $d_k$. We observe that (2.21) bounds the sum rate going across a cut by the conditional mutual information between all sources in $\mathcal{S}$ and all destinations in $\mathcal{S}^c$, given all sources in $\mathcal{S}^c$.

As an example of the cut-set outer bound, consider $K$ source–destination pairs with AWGN links of bandwidth $W$. The channel inputs and outputs are then vectors defined by

$$\mathbf{Y} = \mathbf{H}\mathbf{X} + \mathbf{Z},$$ (2.22)

where **X** is the vector of channel inputs from all the sources with average power constraint $\mathcal{P}$, **Y** is the vector of all channel outputs, **H** $\in \mathbb{R}^{K\times K}$ is the channel gain matrix and **Z** is the vector of independent, unit-variance Gaussian noises at the destinations. The cut-set bound in (2.21) evaluates to [24]

$$\sum_{s_k \in \mathcal{S}, d_k \in \mathcal{S}^c} R_k \leq W \log_2 \det \left(\mathbf{I} + \mathbf{H}(\mathcal{S})\mathbf{K}(\mathcal{S})\mathbf{H}(\mathcal{S}^c)\mathbf{I}\right),$$ (2.23)

where **I** is the identity matrix, $\mathbf{K}(\mathcal{S})$ is the covariance matrix of $\mathbf{X}(\mathcal{S})$ given $\mathbf{X}(\mathcal{S}^c)$, and **H**(S) is determined such that

$$\mathbf{Y}(\mathcal{S}^c) = \mathbf{H}(\mathcal{S})\mathbf{X}(\mathcal{S}) + \mathbf{H}^{T}(\mathcal{S})\mathbf{X}(\mathcal{S}^c) + \mathbf{Z}(\mathcal{S}^c).$$ (2.24)

As another example of the cut-set outer bound, consider the three-node relay channel shown in Fig. 2.7. Assume that links are AWGN links of bandwidth $W$. Let $X_s$ denote the symbol sent from the source, and $X_r$ denote the symbol sent from the relay. Source and relay powers are denoted by $\mathcal{P}_s$ and $\mathcal{P}_r$. The received symbols at the destination and the relay, respectively, are $Y_d$ and $Y_r$. There are two cuts in the network: in the first cut, only the source forms the set $\mathcal{S}$, whereas in the second cut the source and the relay form the set $\mathcal{S}$. The cut-set bound (2.21) evaluates to
