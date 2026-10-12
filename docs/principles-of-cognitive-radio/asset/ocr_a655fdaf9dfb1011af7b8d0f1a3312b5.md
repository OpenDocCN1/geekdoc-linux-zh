The capacity region (2.37) can alternatively be expressed as the intersection of two associated multiple-access channel (MAC) rate regions [18]:

$\mathcal{C}=\bigcup\big\{\mathcal{R}_{\mathrm{MAC}_{1}}\cap \mathcal{R}_{\mathrm{MAC}_{2}}\big\}$.  (2.38)

Recall that the multiple access channel consists of multiple transmitters simultaneously sending to one receiver. In Fig. 2.11, the channel MAC₁ consists of two encoders and decoder 1 and, similarly, the channel MAC₂ consists of two encoders and decoder 2. The capacity region of this network is in general a lower bound on the capacity of the interference channel because both receivers need to decode data sequences sent from both sources. In the opposite channel, in contrast, each receiver decodes data sequences sent from only one source. In strong interference, however, each receiver can decode unwanted data sequences without reducing the capacity region of the interference channel, and the capacity region of the interference channel then coincides with (2.38).

Note that, in strong interference, the capacity is achieved by joint decoding of both data sequences at the decoders. In the special case of *very strong* interference, decoders do not need to perform joint decoding of the data sequences. Instead, interference cancellation can be performed successively, allowing for interference-free decoding of the desired data sequence [10].

We next consider the opposite interference regime in which the interference is weak. In this regime, the interfering data sequence cannot be decoded, but it is not strong enough to significantly degrade the rate of the impacted user. When the interference is weak, intuitively we expect that the optimal decoding strategy is to treat it as noise. However, it has been difficult to prove that this intuition is correct, and hence the capacity remains unknown. Conditions under which treating interference as noise leads to sum-rate capacity in two-user Gaussian channels were determined in [1, 63, 75]. In this regime (termed *noisy interference* in [75]), the cross-channel gains $h_{12}$ and $h_{21}$ in (2.33) as well as the transmit powers $P_{1}$ and $P_{2}$ are small; specifically, they satisfy

$h_{12}(h_{21}^{2}P_{1}+1)+h_{21}(h_{12}^{2}P_{2}+1)\leq 1.  \tag{2.39}$

The sum-rate capacity is then given by [75, Theorem 2]

$C=W \log _{2}\left(1+\frac{P_{1}}{1+h_{12}^{2}P_{2}}\right)+W \log _{2}\left(1+\frac{P_{2}}{1+h_{21}^{2}P_{1}}\right).  \tag{2.40}$

The proof of this result uses a genie-based outer bound for the Gaussian interference channel.

The above described regimes are two extremes with respect to the amount of interference that is being experienced and removed by receivers. Not surprisingly, in strong interference the highest-rate scheme is to decode the unwanted data sequences and subtract their corresponding signals, thus removing their interference from the received signal. In the other extreme of weak interference, the highest-rate strategy is to ignore the interference, that is, treat it as noise.

In regimes that are in between the two extremes, the interference is not strong enough so that decoding of the unwanted data sequence is optimal, nor is it weak enough to