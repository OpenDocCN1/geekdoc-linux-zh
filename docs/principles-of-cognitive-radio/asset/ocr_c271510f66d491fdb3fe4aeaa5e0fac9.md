might not allow the detection of another use if the relevant transfer function is in a fading dip. The FCF tells designers how densely a spectrum has to be sampled to avoid this problem.

For the exponential PDP, (3.43), it is easy to show that $F(\Delta f)=1/[1+(j2\pi\Delta f \tau_0)]$. Note that, given the unit area of $P(\tau)$ and the nature of the Fourier transform, the value of $F(0)$ is always 1, as is appropriate since the fading at any frequency is perfectly correlated with itself.

The coherence bandwidth $B_c$ is defined as the smallest frequency separation such that $|F(B_c)/F(0)|<k$, where $k$ has been given by different authors as 0.5, 0.75, and 0.9. In [32], the coherence bandwidth is related to the delay spread via

$B_c = \frac{\arccos(k)}{2\pi}\frac{1}{\tau_{\mathrm{rms}}}. \tag{3.45}$

For $k=0.5$, this yields $B_c=1/6\tau_{\mathrm{rms}}$. Another approximation, given in [100] for $k=0.5$, is $B_c\approx1/5\tau_{\mathrm{rms}}$. For the case of the exponential PDP (and recalling that, in this case, $\tau_0$ and $\tau_{\mathrm{rms}}$ are the same), it is easy to show for $k=0.5$ that $B_c=\sqrt{3}/2\pi\tau_{\mathrm{rms}}\approx1/3.6\tau_{\mathrm{rms}}$. Clearly, the precise relationship between $B_c$ and $\tau_{\mathrm{rms}}$ depends upon the shape of the PDP, but it is always a reciprocal one.

Finally, the coherence bandwidth gives us another way to distinguish between the "narrowband" and "wideband" cases mentioned in Section 3.8.1.

+   - **"Narrowband"** is the case where the signal bandwidth is small compared to $B_c$; this case is commonly known as *flat fading* (transfer function is flat across the signal bandwidth).
+   - **"Wideband"** is the case where the signal bandwidth is comparable to or greater than $B_c$; this case is commonly known as *frequency selective fading*.

# 3.8.6 A model and values for the delay spread

It follows from the above derivations that the delay spread is obtained from impulse responses taken over an area in which small-scale fading occurs. In different small-scale areas, $\tau_{\mathrm{rms}}$ can take on different values. It is useful to interpret those different values as different realizations of a random variable, and investigate its probability density function. Following [44], $\tau_{\mathrm{rms}}$ is well-approximated as $\tau_{\mathrm{rms}} = T_1 d^{\gamma} y. \tag{3.46}$ where $d$ is in km; $y$ is a lognormal variate whose dB value has zero mean and standard deviation $\sigma_z$ and $T_1$ is the median delay spread at $d=1$ km. Numerical values for the parameters $T_1$, $\gamma$, and $\sigma$ are tabulated in [44] for different environments.

Many measurements for rms delay spread can be found in the literature. Typical values for different environments are as follows (see also [82]).

+   - *Indoor residential buildings* Delay spreads of 5–10 ns are typical, but values up to 30 ns have been measured [38, 69].