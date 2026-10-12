
of rays spaced at τ = i/W, i = 1, 2, 3, … The amplitudes of the rays in the cluster decay exponentially with τ, with the decay constant being variable from one path to another. For every ray in the exponential cluster, the amplitude is an average over local spatial samples, and the pdf of the spatial variability is a Gamma function.

For the exponential-log normal model, reported in [37], the PDP shape is similar to that of the exponential model, except that the exponential cluster is multiplied by a correlated lognormal process over τ. Several parameters of this model are found to be functions of distance along the path. This model is more complicated than the exponential one, requiring more model parameters.

For the cluster model, reported in [79], the PDP is a sum of several exponential clusters, with the starting delay of each cluster being variable from one path to another. Similarly variable are the τ-positions of the rays within each cluster, rather than being uniformly spaced at intervals of 1/W. This model is a variation on the Saleh-Valenzuela cluster model devised for wideband (as opposed to ultra-wideband) indoor channels [95].

In all three of the above PDP models, the major difference from traditional wideband models is that the ray amplitudes are not Rayleigh-fading; because each ray is a sum of just a few MPCs, these amplitudes have narrower fading distributions (e.g., a lognormal pdf with dB standard deviation 3.4 dB, as in [79]). A detailed description of, and comparisons among, the three models is given in [46].

## 3.9 Angle dispersion

### 3.9.1 Directions of arrival and departure

The MPCs are characterized not only by their delays, but also by their directions. An MPC leaves the TX in a certain direction (determined by the location of the first scatterer it will encounter), and arrives at the RX in a certain direction (similarly determined by the position of the last scatterer before arrival). Since there are many MPCs, which can depart and arrive in different directions, a multipath channel leads to angular dispersion. This dispersion is very important for CR. For one thing, it determines the ability of adaptive antennas to transmit into directions such that they will not disturb other users located in certain directions (see Chapter 2). A small angular spread offers the possibility of precisely focusing beams into particular directions.

Conversely, a large angular spread can lead to gain decorrelations, for antenna elements spaced by just a fraction of a wavelength. This phenomenon can aid diversity via use of multiple elements and maximal ratio combining [96, Section 10.5]; or it can increase capacity via multiple co-frequency streams, as in multiple-input/multiple-output (MIMO) links [10]. Such MIMO-based capacity gains can benefit CR systems in the interleaving mode, by offsetting capacity losses caused by remaining silent during primary transmissions. Finally, angular dispersion is strongly related to Doppler, as we have shown in Section 3.7, and therefore influences the temporal variations (correlation times) of CR channel responses.

A description of the angular dispersion can be made by generalizing the concept of impulse response. The double-directional impulse response (DDIR), which generalizes (3.37), again consists of a sum of contributions from the MPCs [105]:

$$h(t,\tau,\Omega,\Psi)=\sum_{n=1}^{N} a_n(t)\delta(\tau-\tau_n)\delta(\Omega-\Omega_n)\delta(\Psi-\Psi_n),\qquad(3.47)$$

with $a_n(t)=|a_n|\exp[j\Phi_{a_n}(t)]$, and where the $\Omega_n$ denote the directions of departure (DODs), the $\Psi_n$ are the directions-of-arrival (DOAs), and $N$ is the number of MPCs.

Equation (3.47) assumes that the MPCs can be represented by ideal homogeneous plane waves, such that they are represented by delta functions in the angular domain (when taking into account wavefront curvature, the delta functions need to be replaced by more general functions). We see the strong analogy between the traditional model, (3.37), and this double-directional representation, where each MPC is additionally characterized by a DOA and DOD.

The double-directional impulse response is an abstract description of the propagation effects alone, without being impacted by the antenna geometry. For the performance analysis of communications systems, we often need the joint impulse response at the elements of an antenna array, which can be represented as a matrix of impulse responses if we have arrays at both link ends, and a vector if we have an array at one link end only.

We now show how to obtain such an impulse response matrix from the double-directional impulse response. This derivation is based on the principle that the contribution of an MPC to the total impulse response at two different antenna elements differs only by a phase factor that is determined by the direction of the MPC and the relative position of the antenna elements. We denote the transmit and receive element coordinates as $\mathbf{r}_T^{(1)},\mathbf{r}_T^{(2)},...,\mathbf{r}_T^{(N_T)}$ and $\mathbf{r}_R^{(1)},\mathbf{r}_R^{(2)},...,\mathbf{r}_R^{(N_R)}$, respectively. For one particular time instant (equivalently, one realization of the $a_n$), the impulse response from the $m$th transmit to the $l$th receive element becomes (under the assumption of plane, narrowband waves)

$$h_{l,m}=h\left(\mathbf{r}_T^{(m)},\mathbf{r}_R^{(l)}\right)=\sum_n a_n g_T(\Omega_n)g_R(\Psi_n)\exp\left(j\mathbf{k}(\Omega_n)\bullet\mathbf{r}_T^{(m)}\right)\exp\left(j\mathbf{k}(\Psi_n)\bullet\mathbf{r}_R^{(l)}\right),\qquad(3.48)$$

where $g_T$ and $g_R$ are the complex (amplitude) patterns of the transmit and receive antenna elements, respectively, $\mathbf{k}$ is the unit wave vector in the direction of the $i$th DOD or DOA, and $\bullet$ denotes the dot product; the summation can be replaced by an integration if the double-directional impulse response has continuous components. We thus see that it is easily possible to obtain the impulse response matrix from a double-directional impulse response (and the knowledge of antenna positions and patterns) while the converse is not true.

The DDIR is a very general description of the channel.⁹ From it, we can derive the "normal" time-variant impulse response by weighting the DDIR with the antenna pattern, and then integrating over all direction angles

$$h(t,\tau)=\iint h(t,\tau,\Omega,\Psi)g_{T}(\Omega)g_{R}(\Psi)d\Omega d\Psi.\tag{3.49}$$

The angular power spectrum (APS) is a characterization of how much power, on average, arrives from (or departs towards) a certain angle. For example, when considering the APS at the RX,

$$APS(\Psi)=\mathbb{E}\{|h(t,\tau,\Omega,\Psi)|^{2}\},\tag{3.50}$$

where the expectation is over t, τ, and Ω. A similar formulation applies to the APS at the TX, APS(Ω). One could also define a spectrum APS(Ψ,τ) as the expectation in (3.50) over just t and Ω. This function reflects the physical reality that the angular power spectrum can be different for different delays. In practice, however, it is often more convenient to include the averaging over τ; this is especially appropriate for narrowband channels, where the MPCs overlap.

A major simplification of APS(Ψ) is made possible by noting that most MPC arrival directions at an RX lie in or close to the horizontal plane containing the antenna. Thus, there is no spread with respect to elevation angle, θ. In this case, APS(Ψ) can be reduced to a power spectrum over azimuth angle, φ, at the receiver. Referring to Section 3.7, this can be seen as equivalent to S_φ(φ) in (3.31) or a continuous version thereof. For convenience, and with this equivalence in mind, we will use the notation APS(φ) in the present discussion.

Finally, a compact characterization of the angular dispersion is given by the rms angular spread, henceforth simply called "angular spread," AS [33]. We will focus on the angular spread at the RX. This quantity is the second central moment of the APS normalized to have an area of 1 over (−π,+π). We have seen that, because of angular dispersion, there is space-selective fading of received amplitudes about the RX location. The correlation distance associated with this fading has an inverse relationship to the AS.

### 3.9.2 Models for the APS shape and angular spread

We start with the case of an elevated TX or RX, e.g., as on a base station, mostly above the clutter. Here, the most common model for the APS is a small angular spread around the nominal line-of-sight direction, usually with a Laplacian shape [89],

$$APS(\phi)=\exp\left[-\sqrt{2}\frac{|\phi-\phi_{0}|}{\phi_{\mathrm{rms}}}\right],\tag{3.51}$$
