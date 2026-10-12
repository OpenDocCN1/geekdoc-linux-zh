fundamental to the understanding of microwave measurements. See **Microwave**. At any reference plane in a transmission line there are considered to exist two independent traveling electromagnetic waves moving in opposite directions. One is called the forward or incident wave, and the other the reverse or reflected wave. The electromagnetic wave is guided by the transmission line and is composed of electric and magnetic fields with associated electric currents and voltages. Any one of these parameters can be used in considering the traveling waves, but the measurements in the early development of microwave technology made principally on the voltage waves led to the custom of referring only to voltage. One parameter in very common use is the voltage reflection coefficient $\Gamma$, which is related to the incident, $V_i$, and reflected, $V_r$, voltage waves by Eq. (1).

$$ \Gamma = \frac{V_r}{V_i} \quad\quad\quad\quad\quad\quad\quad\quad\quad (1) $$

# **Impedance.**

The voltage reflection coefficient $\Gamma$ is related to the impedance terminating the transmission line and to the impedance of the line itself. If a wave is launched to travel in only one direction on a uniform reflectionless transmission line of infinite length, there will be no reflected wave. The input impedance of this infinitely long transmission line is defined as its characteristic impedance $Z_0$. An arbitrary length of transmission line terminated in an impedance $Z_L$ will also have an input impedance $Z_0$. See **ELECTRICAL IMPEDANCE.**

If the transmission line is terminated in the arbitrary complex impedance load $Z_L$, the complex voltage reflection coefficient $\Gamma_L$ at the termination is given by Eq. (2).

$$ \Gamma = \frac{Z_L - Z_0}{Z_L + Z_0} \quad\quad\quad\quad\quad\quad\quad\quad\quad (2) $$

Even when there is no unique expression for $Z_L$ and $Z_0$ such as in the case of hollow conductor waveguides, the voltage reflection coefficient $\Gamma$ has a value because it is simply a voltage ratio. In general, the measurement of microwave impedance is the measurement of $\Gamma$. Both amplitude and phase of $\Gamma$ can be measured by direct probing of the voltage standing wave set up along a transmission line by the two opposed traveling waves, but this is a slow technique. Directional couplers have been used for many years to perform much faster swept frequency measurement of the magnitude of $\Gamma$, and more recently the use of automatic network analyzers under computer control has made possible rapid, accurate measurements of amplitude and phase of $\Gamma$ over very broad frequency ranges. See **DIRECTIONAL COUPLER.**

# **Power.**

A required increase in microwave power is expensive whether it is the output from a laboratory signal generator, the power output from a power amplifier on a satellite, or the cooking energy input from a microwave oven. To minimize this expense, absolute power must be measured. Most techniques involve con-version of the microwave energy to heat energy which, in turn, creates a temperature rise in a physical body. This temperature rise is measured and is approximately proportional to the power dissipated. The whole device can be calibrated by reference to low-frequency electrical standards and application of appropriate corrections. See **RADIOMETER.**

The power sensors are simple and can be made to have a very broad frequency response. A power meter can be connected directly to the output of a generator to measure available power $P_a$, or a directional coupler may be used to permit measurement of a small fraction of the power actually delivered to the load.

# **Scattering coefficients.**

While the measurement of absolute power is important, there are many more occasions that require the measurement of relative power which is equivalent to the magnitude of voltage ratio and to measure attenuation. Also this arises frequently the need to measure the relative phase of two voltages. Measurement systems having this capability are referred to as vector network analyzers, and they are used to measure scattering coefficients of multi-port devices. The concept of scattering coefficients is an extension of the voltage reflection coefficient applied to devices having more than one port. The most simple is a two-port. Its characteristics can be specified completely in terms of a $2 \times 2$ scattering matrix, the coefficients of which are indicated in the illustration. The incident voltage at the reference plane of each port is defined as $a$, and the reflected voltage is $b$. Voltages $a$ and $b$ are related by matrix equation (3), where ($S_{mn}$) is the scattering matrix of the junction. Writing Eq. (3) out for a two-port device gives Eqs. (4) and (5). Examination of Eq. (4) shows, for example, that $S_{11}$ is the voltage reflection coefficient looking into port 1 if port 2 is terminated with a $Z_0$ load ($a_2 = 0$). See **MATRIX THEORY.**

$$ \begin{bmatrix} b_1 \\ b_2 \end{bmatrix} = (S_{mn}) \begin{bmatrix} a_1 \\ a_2 \end{bmatrix} \quad\quad\quad\quad\quad\quad\quad\quad\quad (3) $$
$$ b_1 = S_{11}a_1 + S_{12}a_2 \quad\quad\quad\quad\quad\quad\quad\quad\quad (4) $$
$$ b_2 = S_{21}a_1 + S_{22}a_2 \quad\quad\quad\quad\quad\quad\quad\quad\quad (5) $$

# **Heterodyne.**

The heterodyne principle is used for scalar attenuation measurements because of its large dynamic range and for vector network analysis because of its phase coherence. The microwave signal at frequency $f_{RF}$ is mixed with a microwave local oscillator at frequency $f_{LO}$ in a nonlinear mixer. The output signal at frequency $f_{IF} = f_{LO} - f_{RF}$ is faithful amplitude and phase reproduction of the original microwave signal but is at one, fixed frequency so that it can be measured simply with low-frequency techniques. One disadvantage of the heterodyne technique at the highest microwave frequencies is its cost. Consequently, significant effort has been expended in development of multiport network analyzers which use several simple power detectors and a computer analysis approach that allows measurement of both relative voltage amplitude and phase with required hardware cost. See **HETERODYNE PRINCIPLE.**

# **Noise.**

Microwave noise measurement is important for the communications field and radio astronomy. The measurement of thermal noise at microwave frequencies is essentially the same as low-frequency noise measurement, except that there will be impedance mismatch factors which must be carefully evaluated. The availability of broadband semiconductor noise sources having a stable, high, noise power output has greatly reduced the problems of source impedance mismatch because an impedance-matching attenuator can be inserted between the noise source and the amplifier under test. See **ELECTRICAL NOISE; ELECTRICAL NOISE GENERATOR; MICROWAVE NOISE STANDARDS.**

# **Use of computers.**

The need to apply calculated corrections to obtain the best accuracy in microwave measurement has stimulated the adoption of computers and computer-controlled instruments. An additional benefit of this development is that measurement techniques that are superior in accuracy but too tedious to perform manually can now be considered. For a discussion of attenuation in microwave circuits see **ATTENUATION** (ELECTRICITY).

![](bbox=[0.07, 0.75, 0.48, 0.95])