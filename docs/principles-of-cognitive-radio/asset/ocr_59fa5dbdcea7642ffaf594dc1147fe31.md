\hat{h}(t, \tau) = \sum_{m} c_{m}(t)\xi(\tau - m/W). \tag{3.40}

To write an expression for c_m(t), we refer to the inner sum of (3.38) and consider the time variation of the nth MPC, with complex gain a_n and arrival time τ_n. For the normal geometry of a TX-RX path and its nth scatterer, the amplitude |a_n| and arrival time τ_n change very little in the neighborhood of a mobile's position, i.e., over a travel distance of many wavelengths. By contrast, the phase of a_n changes rapidly, i.e., by 360° for every travel distance of λ relative the scatterer. Thus, over a travel distance of many wavelengths, corresponding in time to a great many digital symbols,⁶ the mth tap gain can be written as

c_m(t) = \sum_{n} |a_n| \exp(j\phi_{a_n}(t))\xi(m\Delta - \tau_n). \tag{3.41}

Assuming as before that the dominant terms in this sum (those peaking in an interval of width Δ about mΔ) are numerous, c_m(t) can be regarded as a complex Gaussian temporal process. In addition, the mth tap has its own angular power spectrum (based on the set of arrival angles for the MPCs in the mth bin) and, under mobility, its own associated Doppler spectrum. Even so, in most system studies, it is conventional to assign the same Doppler spectrum to all taps of the TDL representation, usually the one for uniform angle-of-arrival distribution, (3.34).

# 3.8.4 The power delay profile, P(τ)

For the assumed complex Gaussian statistics, the MPC phases are uniformly random over the small-scale fading, and the mean of c_m(t) is zero. Then, the only parameter needed to characterize the first-order statistics of c_m(t) is its mean-square value. This raises the topic of power delay profile (PDP), which plays a prominent role in analyzing and simulating wireless channels.

A formal mathematical definition of the PDP is

\mathcal{P}(\tau) = (1/W) \mathbb{E}_t \{ |\hat{h}(t, \tau)|^2 \}, \tag{3.42}

where \mathbb{E}_t denotes expectation over a time interval where small-scale fading happens.⁷ This formal definition can run into mathematical problems when \hat{h}(t, \tau) is a discrete sum of impulses, bandlimited or otherwise. One popular alternative is to define the PDP itself as a sum of impulses along the τ-axis, having the delays of the MPCs (τ₁, ..., τ_N) as in (3.37), and with the power P_n at delay τ_n being |a_n|². This approach is especially useful in ultra-wideband channels, where the individual MPCs are resolvable in delay. For more conventional wideband channels with many MPCs per delay bin (the case considered here), the PDP can instead be a sum of impulses at