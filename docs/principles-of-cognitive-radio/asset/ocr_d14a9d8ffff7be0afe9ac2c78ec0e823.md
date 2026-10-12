# 2.7 Overlay cognitive radio networks

![](bbox=[0.27, 0.13, 0.81, 0.26])

Figure 2.18 A channel with a random state. The state $S^n$ is known noncausally at the encoder.

increasing its rate. In the overlay channel, since the cognitive encoder has perfect knowledge of the data sequence and the encoding strategy of the primary user, the secondary transmitter–receiver pair can view this situation as communication in a channel with a random state noncausally known at the encoder, also known as the Gelfand–Pinsker problem [30], shown in Fig. 2.18. In this figure, a single source communicates a data sequence $W \in \{1, \ldots, 2^{nR}\}$ to the destination over a channel given by $p(y|x, s)$. The channel state sequence $S^n$ is assumed to be a random iid sequence generated from the distribution $p(s)$ over the random state. $S^n$ is noncausally known at the encoder.

We next consider an AWGN channel where the random state is an additional interference term $S$. Specifically, an AWGN channel with a random interference state has input–output relationship given by

$Y = X + S + Z, \tag{2.68}$

where $Z$ is zero-mean Gaussian noise at the receiver with power $\mathcal{N}$ and $S$ is zero-mean Gaussian noise at the receiver with power $\mathcal{N}_s$. The transmit power constraint is $\mathbb{E}[X^2] \le \mathcal{P}$. The Gelfand–Pinsker encoding in this channel model reduces to DPC, described above for the interference channel, whereby precoding is used to cancel the effect of the interference term $S$. In this setting DPC achieves the capacity of the AWGN channel as if there were no interference, i.e., it completely cancels the effect of interference $S$, yielding capacity

$C = W \log_2 \left( 1 + \frac{\mathcal{P}}{\mathcal{N}} \right) . \tag{2.69}$

The capacity of the general discrete-time memoryless channel with random state is given by

$C = \max_{p(u|x), f(.)} I(U;Y) - I(U;S), \tag{2.70}$

where $U \to (X, S) \to Y$ form a Markov chain, and is achieved by Gelfand–Pinsker encoding [30]. The random variable $U$ is used to generate a codebook at the encoder such that, in each block transmission, the codeword depends both on the data sequence and on the random state $S^n$. Gelfand–Pinsker encoding can play a crucial role in overlay cognitive radio, as will be described next.