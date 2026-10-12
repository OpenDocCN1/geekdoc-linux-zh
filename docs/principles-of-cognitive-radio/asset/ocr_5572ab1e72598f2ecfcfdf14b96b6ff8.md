secondary link, where these parameters now vary over time. It is shown in [31] that the ergodic capacity of the secondary user channel under an average interference power constraint imposed by the primary system yields

$$ C = \iint W \log_2 \left( \frac{ |h_s|^2 }{ |h_{ps}|^2 W N_0 \lambda } \right) p(h_s) p(h_{ps}) dh_s dh_{ps}, $$

The optimal power allocation for the secondary user that achieves this capacity is given by

$$ P^* = \left( \frac{ 1 }{ \lambda |h_{ps}|^2 } - \frac{ N_0 W }{ |h_s|^2 } \right)^+, $$

where $\lambda$ is determined to satisfy the received power constraint as

$$ \iint \left( \frac{ 1 }{ \lambda } - N_0 W \frac{ |h_{ps}|^2 }{ |h_s|^2 } \right)^+ p(h_s) p(h_{ps}) dh_s dh_{ps} = \eta. $$

This optimal power allocation is similar to the time water-filling given by (2.16) under a transmit power constraint. However, imposing a power constraint at the primary receiver results in a time-varying water level inversely proportional to $|h|^2$, the magnitude squared of the instantaneous time-varying channel gain. Moreover, the cutoff fade depth below which no data is transmitted by the secondary user depends on both their channel gain $h_s$ and the gain $h$ between the secondary transmitter and primary receiver. In particular, the secondary user increases his transmit power when either $h_s$ increases (as their channel is better, i.e., conventional water-filling) or when $h$ decreases, since less interference is caused to the primary. Note that, from (2.55), the capacity depends on channel statistics from the secondary transmitter to both primary and secondary receivers. Interestingly, it is shown in [31] that the capacity (2.55) when both $h_s$ and $h$ experience Rayleigh fading is larger than the capacity of the corresponding AWGN channel with the same average SNR. However, with this Rayleigh fading on both channels, the average SNR is low, and it is known that at low SNRs the ergodic capacity of a Rayleigh fading channel exceeds that of an AWGN channel with the same SNR [32, Figure 4.7]. Note, however, that this is in some sense an artifact of the infinitely long tail probability of the Rayleigh distribution, which results in a set of very high SNR channels with very low probability. These rare high-SNR channels can be exploited by allocating significant power and rate during these low probability events, which results in a slightly higher capacity than a static channel maintaining a fixed rate commensurate with the same average SNR. Note, also, that the propagation characteristics which induce fading also cause some reduction in average received power. Hence, comparing fading and nonfading channels with the same average SNR does not fully capture the impact of fading on performance.

Under the peak constraint (2.44), the optimum power strategy for the secondary user is simply to transmit at the highest power allowed by (2.44). The capacity is then given by

$$ C = \iint W \log \left( \frac{ |h_s|^2 }{ |h_{ps}| W N_0 \lambda } \right) p(h_s) p(h_{ps}) dh_s dh_{ps}. $$