
![](img/2d42983cf592ef4fc8a22646ddc49799_137_0.png)

(a) Scatter plot of path loss vs. distance and a linear fit

![](img/2d42983cf592ef4fc8a22646ddc49799_137_1.png)

(b) CDF of shadow fading

Figure 3.2 Path loss and shadow fading for cellular signals in a suburban environment.

(circles) from the straight line were used to form a population of deviations, whose CDF is plotted in the lower figure. Also shown is a Gaussian CDF with the same mean (namely, 0) and standard deviation (≈ 5.8 dB). The agreement between the two CDFs is excellent.

The variable quantity S is called shadow fading, for historical reasons. In the early days of cellular radio, the fluctuation of path loss about a linear growth with log-distance was attributed to the shadowing effect of obstructions (e.g., buildings) between the base station and the mobiles. It has since been learned, however, that the fluctuations occur even on paths with a clear line-of-sight but with reflections along the path, e.g., in LOS microcells [41]. We will continue to refer to this random-like process by its popular name. We note that, since S is Gaussian, the factor ζ in (3.7) is log-normal; hence, the popular terminology in the literature for the variation about the median is lognormal shadow fading.

A popular convention among wireless engineers is to regard the bracketed term in (3.8) as the "path loss," to which shadow fading (S) is added, as if the former is a natural attribute of the distance and environment and the latter is a perturbation. In reality, the separation into these parts is merely an artifact of the measurement program (which locations are measured and how many) and the data processing used (least-squares fitting of a linear function of log-distance). We will use here the more precise convention that the bracketed term represents a median path loss for distance d in a given environment; and the path loss at distance d is the sum of both this median and a zero-mean, random-like component called shadow fading. The most widely used formulation for the median path loss, as discussed later, is in [53].

## 3.4.2 Shadow fading, S

The standard deviation (σ) of S can vary from 3 to 12 dB, depending on the environment. In a typical cellular environment, the most commonly used value is 8 dB; for indoor environments, it is ~ 4 dB. This description summarizes the first-order statistics of shadow fading and is well supported by measurements. Less well documented are the second-order statistics of shadow fading, e.g., the autocorrelation function of its 2-dimensional distribution over space for a specified TX location. This information is not always needed in system studies, but one can envision CR scenarios where it would be useful. For example, in an environment where n CR nodes are receiving and one source (either primary or CR) is transmitting, simulating the path losses to the n CR nodes would require knowing the n × n correlation matrix among the n source-to-node shadow fading components. It is easy to appreciate the complexity of the measurement programs needed to derive such information, which explains the sparse literature on the subject.

Nevertheless, we can cite a few useful results pertaining to the spatial distribution of shadow fading. One is due to Gudmundson [47], who reported that, along a path moving towards or away from the TX in the x direction, the correlation between S-values for points at x and x + Δx can be approximated by

```
E_x{ S(x) S(x + Δx) } = σ² exp( -|Δx| / X_c ) = ρ(Δx). (3.10)
```

where X_c is the "correlation distance" of shadow fading. Typical values for X_c range from 10 m (i.e., in urban microcells) to 500 m (i.e., in some rural macrocells). Roughly speaking, X_c is a measure of how far a mobile must travel before it encounters a different set of obstructing or scattering objects. In CR environments where sensor networks are used to obtain and update radio maps of the environment, the correlation distance is an important parameter for determining the necessary density of sensors. This correlation function for shadow fading along a path has been widely used, in part because it was among the first to be reported; in addition, it is simple to describe, and is readily simulated via an AR(1) process [54]. However, other empirically-derived functions have been proposed that work better in some environments. For example, see [116], which expresses ρ(Δx) – when averaged over many routes – as a sum of two decaying exponentials in |Δx|; and expresses ρ(Δx) for individual routes as an exponential combined with a sinusoid.

Besides the need to estimate shadow fading correlations along a single path, there can be a need to correlate the shadow fading values on two paths, as when one radio is communicating with two other radios. In such cases, the angle between the two paths becomes important in addition to distances, see [2, 42, 112]. A simple approach often used in cellular system simulations is to assume that the shadow fading, S1 and S2, from any two bases to the same mobile are correlated Gaussian variables, with the correlation coefficient being ~ 0.5 [107].

Other measurements and models relating to the properties of S have also been reported. Here, we briefly summarize those of major import.

- In the model of PL vs. d, (3.8), the standard deviation of S can vary with distance along the TX-RX path. Specifically, it tends to be smaller at close-in distances, where the path loss is close to that of free space, with little variation; and it can grow with distance, leveling off to a final value. To capture this effect, a model is given in [55] which we rewrite here as
  
  σ(d) = 1.5 + σ_m [ 1 - exp( - |PL_med(d) - FSPL(d)| / 4 ) ] , (3.11)
  
  where σ_m is a data-derived fitting parameter.
- We also know that shadow fading is a “semi-local” phenomenon, in the sense that, from one local environment to another, the urban or natural terrain can change character (e.g., from built-up neighborhoods to parks), leading to a different value for σ. This effect is partially quantified in [27], which reports results at 1.9 GHz from drive measurements in 95 environments located around the United States. The outcome is a probability distribution for σ for each of three representative kinds of terrain. For each terrain category, the variability among cells is shown to be describable by a truncated Gaussian distribution.
- Finally, σ changes very slowly with frequency. Though there are few if any explicit measurements tracking its value across bands, there is anecdotal evidence that σ increases slightly with frequency. This is likely due to the greater diffraction losses at higher frequencies, so that the presence/absence of obstructions magnifies the spread of path loss values in a cell.

## 3.4.3 Median path loss, PLmed

Many papers, reports and standards documents have been published on the median path loss, PLmed (e.g., [27, 53]). The vast majority use the bracketed term in (3.8) as the generic form. We note, however, that some formulas contain “break points” in distance, d, where the value of γ changes; and some formulas for indoor environments add one or more terms to capture the effects of transmission through floors and walls [92]. Primarily, though, what distinguishes one set of authors from another is how they characterize A and γ. We will describe here two median path loss models in some depth. In so doing, we hope to illustrate, by concrete examples, the nature of such models for wireless systems.

For cellular systems in particular, the most popular model is the one developed by Hata [53] based on extensive measurements made by Okumura in the Tokyo area in the 1960s [85]. The model covers distances from 1 to 20 km; frequencies from 150 MHz to 1.5 GHz; base antenna heights from 30 to 200 m; and mobile antenna heights from 1 to 10 m. The environments covered are urban areas (large cities and medium-small cities); suburban areas; and open areas. In the 1990s, as personal communications services (PCS) opened up worldwide near 2 GHz, the Hata-Okumura model was expanded to include frequencies up to 2 GHz, and small urban cells (diameters below 1 km). This expansion, developed by the European Cooperative for Scientific and Technical Research, is the COST 231–Hata model [111].

The original Hata–Okumura model is applicable to wide-area scenarios wherein the user terminals are mobile. A situation like this is suitable for cognitive radio scenarios where the delay tolerance of the service is high. For urban environments and user terminals at height 1.5 m, the formula for PLmed is identical to the bracketed quantity in (3.8), where d0 = 1 km;

A = [69.55 + 26.16 log₁₀ f_c − 13.82 log₁₀ h_b]; (3.12)

and

γ = [4.49 − 0.655 log h_b]. (3.13)

In these formulas, f_c is the carrier frequency in MHz and h_b is the base antenna height in meters. The model provides additive terms to A that adjust it for terminal heights different from 1.5 m and environments different from urban. For similar CR applications over a smaller area (radii less than 1 km) and frequencies closer to 2 GHz, COST 231–Hata is more applicable. The term 26.16 log₁₀ f_c in A is largely due to the antenna aperture effect in all path loss equations, including the one for free-space propagation, which accounts for 20 log₁₀ f_c; the remaining part, 6.16 log₁₀ f_c, is due to radio wave diffraction around obstructing objects along the radio path, causing an incremental loss that increases with frequency.

The Erceg path loss model, devised for fixed wireless applications [27], was cited in Section 3.4.2 in connection with shadow fading. A CR context for this model might be transmission to and from fixed sensors (e.g., as used for radio mapping) distributed over a wide area. The model was derived from 1.9 GHz data collected from 95 suburban/residential areas, all with radii of 2 km or less and all downlink terminals at 2-m height. The data span a variety of base antenna heights and terrain types, and the model delineates their influences. Extensions to other carrier frequencies and terminal heights can be made via simple scaling laws, e.g., see [25].
