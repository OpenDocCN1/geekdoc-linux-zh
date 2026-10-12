$$I(X ; Y) \stackrel{\Delta}{=} \int_{\mathcal{X}, \mathcal{Y}} p(x, y) \log \left(\frac{p(x, y)}{p(x) p(y)}\right) d x d y, \tag{2.3}$$

where the integral is taken over the set of possible values $\mathcal{X}, \mathcal{Y}$ for the random variables $X$ and $Y$, respectively, which are also called the input and output **alphabets**, and $p(x)$, $p(y)$, and $p(x, y)$ denote the pdfs of the random variables. When the input and output alphabets $\mathcal{X}$ and $\mathcal{Y}$ are finite, the integral becomes a summation over their joint pmf:

$$I(X ; Y)=\sum_{\mathcal{X}, \mathcal{Y}} p(x, y) \log \left(\frac{p(x, y)}{p(x) p(y)}\right) . \tag{2.4}$$

The log function is typically with respect to base 2, in which case the units of mutual information are bits per channel use, since input $\mathcal{X}$ and output $\mathcal{Y}$ correspond to a single use of the channel.

Shannon proved that the capacity of a large class of single-user time-invariant channels is equal to the mutual information of the channel maximized over all possible input distributions:

$$C=\max _{p(x)} I(X ; Y)=\max _{p(x)} \int_{\mathcal{X}, \mathcal{Y}} p(x, y) \log \left(\frac{p(x, y)}{p(x) p(y)}\right) d x d y, \tag{2.5}$$

For a real discrete time-invariant additive white Gaussian noise (AWGN) channel with bandwidth $W$, received signal power $\mathcal{P}$, and receiver noise PSD $N_{0}$, the channel is described by the input-output relationship

$$Y=X+Z, \tag{2.6}$$

where $X$ is the channel input, $Y$ is the channel output, and $Z$ is the noise introduced by the channel. The capacity-achieving input distribution $p(x)$ for this channel is Gaussian, and results in the channel capacity

$$C=\frac{1}{2} \log _{2}\left(1+\frac{\mathcal{P}}{N_{0} W}\right) \quad \text { bits/channel use. \tag{2.7}$$

The units of bits per channel use are alternatively referred to as bits per dimension. The dimension of a scalar channel with bandwidth $W$ over transmission time $T$ is $2 W T$. Channels with additional dimensions, e. g., MIMO channels with $M$ spatial dimensions, have dimension $2 M T$. Defining capacity in terms of bits per channel use or dimension is typical for multidimensional channels such as MIMO channels, and we will follow this convention. In system designs the data rates are typically given in terms of bits per second. We can convert bits per channel use (corresponding to $2 W T$ dimensions) to bits per second (corresponding to $2 W$ dimensions over $T$ seconds) by multiplying (2.7) by $2 W$, which yields the capacity expression

$$C=W \log _{2}\left(1+\frac{\mathcal{P}}{N_{0} W}\right) \quad \text { bits/second. \tag{2.8}$$

When the channel has attenuation $h$, so that $Y=h X+Z$, its capacity becomes

$$C=W \log _{2}\left(1+\frac{|h|^{2} \mathcal{P}}{N_{0} W}\right) \quad \text { bits/second. \tag{2.9}$$