For suburban environments, the Type-D path category is appropriate, and the path loss for this case is described in Section 2.1.2.2 of [55] as a suburban macrocell model for above rooftop (ART) propagation. The model is similar to the Erceg model [27], as standardized in [25]. For urban environments, the Type-H path category is appropriate, as described in Section 2.1.2.6 of [55]. Here, the underlying model is a modified form of COST 231–Walfisch–Ikegami [111], which captures the over-the-rooftop transmissions of urban environments but excludes the final rooftop-to-street loss of the original model.

Some path loss results for Type-D and Type-H paths are given in Fig. 3.4 for a transmitting antenna height of 30 m, a receiving antenna height of 10 m, and f_c = 600 MHz. Additional parameters h_roof =15 m and b =30 m are given in the urban model for the height of the rooftop and the distance between buildings, respectively. We note that these two models have not been empirically validated, although they build on prior measurement/modeling efforts for geometric scenarios with similar features.

# 3.6 Small-scale fading and the Ricean K-factor

We now turn our attention to the small-scale fading term, \hat{h}(\tau; \mathbf{x}, \mathbf{F}). Recall that \mathbf{x} denotes the set of coordinates on the terrain for the TX and RX; and \mathbf{F} denotes the frequency interval of the signal of interest, with center frequency f_c and bandwidth W. To facilitate understanding, this initial treatment of small-scale fading will consider the extreme case where W shrinks to 0, i.e., small-scale fading for a single frequency, f_c. Later sections will generalize our treatment to the wideband case.

It is obvious that, for a single frequency, \hat{h}(\tau; \mathbf{x}, \mathbf{F}) becomes just a constant over \tau, dependent on \mathbf{x} and f_c. In short, it becomes the (normalized, complex) frequency response at f_c for the path between the TX and RX whose coordinates are given by \mathbf{x}. Thus, we can use the notation

\hat{h}(\tau; \mathbf{x}, \mathbf{F}) \rightarrow \tilde{H}(f_c; \mathbf{x}); single-frequency case. (3.16)

Here, we will elaborate on the statistical variation of this complex amplitude over space in the vicinity of the location coordinates \mathbf{x}. For concreteness, we assume that the TX is at the base and fixed, and the RX is at the mobile and may be moving in the vicinity of its nominal location. If it does move, then the complex amplitude will vary with time as \mathbf{x} does.

# 3.6.1 Spatial variation of field strength

As noted, the electric field strength fluctuates rapidly over space if there is multipath scatter, as in typical wireless environments. This is because the field at a particular point is the sum of several components, as seen in the example of Fig. 3.5, where the mobile is moving to the right with velocity v. The receiving antenna sees the sum of