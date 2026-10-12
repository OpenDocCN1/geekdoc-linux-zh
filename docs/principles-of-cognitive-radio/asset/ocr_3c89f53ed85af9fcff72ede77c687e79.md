Thus, the received signal is the sum of N MPCs at slightly different frequencies. The result is a random-like variation over time of the envelope of the sum. This is just another (more mathematical) way of explaining the small-scale spatial fading described in Section 3.6. Note that, in light of reciprocity, this fading occurs in both directions, i.e., including transmissions from the mobile to the base. For each MPC, with arrival angle φ_n, there is a received power, P_n. The pairing of the set P_n with the set {φ_n} is called the angle-of-arrival (AOA) spectrum,

$S_{\phi}(\phi) = \sum_{n} \rho_n \delta(\phi - \phi_n); \quad -\pi < \phi \le \pi; \quad n = 1, N, \tag{3.30}$

where the ρ_n are the P_n normalized so that they sum to 1. Corresponding to the set {φ_n} is the set of Doppler frequencies, {ν_n}, as given above. Pairing the two sets ρ_n and {ν_n} gives us the Doppler spectrum, S_ν(ν), where ν ranges from −v/λ to v/λ. For future reference, we designate v/λ as ν_max, the magnitude of the largest possible Doppler frequency.

Now consider the case where the AOA spectrum is defined over a continuum of angles. We can then write the Doppler spectrum as

$S_{\nu}(\nu) = \left[ S_{\phi}(\phi^+) + S_{\phi}(\phi^-) \right] \left| \frac{d\nu}{d\phi} \right|^{-1}, \tag{3.31}$

where, from (3.28),

$\phi^+ = \left| \cos^{-1}\left( \frac{\nu}{\nu_{\max}} \right) \right|; \quad \phi^- = -\left| \cos^{-1}\left( \frac{\nu}{\nu_{\max}} \right) \right|; \tag{3.32}$

and

$\left| \frac{d\nu}{d\phi} \right| = -\nu_{\max} \sin \phi = \nu_{\max} \left[ 1 - \left( \frac{\nu}{\nu_{\max}} \right)^2 \right]^{\frac{1}{2}}, \tag{3.33}$

for both φ = φ^+ and φ = φ^-. The two parts of (3.31) are due to the symmetric nature of the cosine function, resulting in the fact that each ν corresponds to two angles (equal and opposite) on the interval (−π, π]. As an example of the Doppler spectrum, assume that S_φ(φ) is uniform over all φ. The Doppler spectrum in this case is

$S_{\nu}(\nu) = \frac{1}{\pi \nu_{\max}} \left[ 1 - \left( \frac{\nu}{\nu_{\max}} \right)^2 \right]^{-\frac{1}{2}}; \quad |\nu| < \nu_{\max}. \tag{3.34}$

This is the well-known Doppler spectrum of Clarke [15] and Jakes [56]. It has the shape shown in Fig. 3.7a. For other angular distributions (i.e., other AOA spectra), the more general formula (3.31) can be used to obtain the Doppler spectrum.

# 3.7.3 The autocorrelation function, A(Δt)

The random-like variation of the signal envelope as a terminal moves over the local terrain at constant velocity v has the same first-order statistics in time as in space, as the