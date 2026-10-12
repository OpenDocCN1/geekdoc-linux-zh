increased intercarrier interference (ICI). Extensive work has been done in designing robust algorithms that estimate the carrier frequency and symbol timing with high accuracy [19, 80, 87] to ensure reliable communication. For NC-OFDM systems however, the imperfect estimation of timing information aggravates the synchronization problem. In some scenarios when users occupy multiple noncontiguous subbands and have large differences in the timing offsets between their transmitters and receivers, cyclic prefix-based timing acquisition algorithms can perform quite poorly. Thus, there is a need for better algorithms of reasonable complexity, or entirely different approaches to symbol timing acquisition.

In a typical OFDM transmitter with $n_\mathrm{B}$ subcarriers, the IDFT modulated symbols can be represented as

```
$x_n= \frac{1}{n_\mathrm{B}} \sum_{k=0}^{n n-1} X_k e^{j2 \pi k n / n_B}, \; n=0, 1, \ldots, N-1.$
```

In an NC-OFDM system, the secondary transmission is only on vacant subcarriers. The subcarriers that are occupied by the primary users are nulled, and hence $X_k=0$ for those subcarriers.

If we assume that an NC-OFDM symbol is $n_\mathrm{B} + p$ samples long with the first $p$ samples, called the cyclic prefix, being the same as the last $p$ samples. The received samples $y_n$ in the presence of timing offset $\tau$ between transmitter and receiver is

```
$y_n=\sum_{l=0}^{m} h_l x_{n-\tau-l}+I_n+w_n, \; n=0, \ldots, N-1,$
```

where $h_l, \; l=0, \ldots, m$ represents the complex $m$-tap frequency selective channel gains, $I_n$ represents the interference from the other users at the receiver, and $w_n$ is the discrete-time noise process at the receiver. Timing acquisition is about estimating the OFDM symbol boundary by estimating $\tau$ at the receiver.

In an NC-OFDM system, the signals $x_n$ and $I_n$ occupy different sets of tones. But, due to practical limitations on pulse-shaping filters they are not ideally band-limited, part of the symbol energies may spill over to the adjacent bands, causing interference. Therefore, performance of timing acquisition algorithms can be improved if wider guard bands are allowed between the signals of the different users. In licensed spectrum, where secondary users opportunistically use the primary spectrum, guard bands protect the primary users from interference caused by the secondary users. In unlicensed spectrum however, uncoordinated access can lead to high occupancy of spectrum. This can result in poor timing acquisition performance [1].

Another design challenge in OFDM systems is the peak-to-average power ratio (PAPR) problem. In general, an OFDM signal is the sum of several signals modulated by sinusoidal waveforms. If the signals are coherently added up, the OFDM signal can have a large peak but the mean power will remain small. Moreover, when the time domain signal traverses from low instantaneous power waveform to a high power waveform, large signal amplitude swings are encountered. This results in high out-of-band harmonic distortion power, unless the transmitter’s power amplifier exhibits linearity