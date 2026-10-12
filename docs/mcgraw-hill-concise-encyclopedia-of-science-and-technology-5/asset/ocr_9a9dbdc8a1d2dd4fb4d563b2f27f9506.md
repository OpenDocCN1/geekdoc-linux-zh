as an output voltage $V_{\text{o}} = K V_{\text{i}}$ from an input voltage $V_{\text{i}}$. This input voltage is obtained from a source voltage $V_{\text{s}}$ with source resistance $R_{\text{s}}$ via voltage division with the amplifier’s input impedance $z_{\text{i}}$. The load voltage $V_{\text{L}}$ across the load impedance $Z_{\text{L}}$ is obtained from $V_{\text{o}}$ via voltage division with the amplifier’s output impedance $z_{\text{o}}$. The input voltage and load voltage are given by Eqs. (1), where $k_{\text{i}}$ and $k_{\text{o}}$, respectively, express the effects of the voltage division loading the source and of the load impedance loading the amplifier. The impedances $z_{\text{i}}$ and $z_{\text{o}}$ mostly consist of a resistor in parallel with a capacitance; often they may be assumed to be purely resistive: $z_{\text{i}} = r_{\text{i}}$ and $z_{\text{o}} = r_{\text{o}}$. From Eq. (1), the amplifier’s operation is given by Eq. (2). Thus, the amplification is decreased

```
$$
\begin{align}
V_{\text{i}} & = \frac{z_{\text{i}}}{z_{\text{i}} + R_{\text{s}}} V_{\text{s}} = k_{\text{i}} V_{\text{s}} \\
V_{\text{L}} & = \frac{Z_{\text{L}}}{Z_{\text{L}} + z_{\text{o}}} V_{\text{o}} = k_{\text{o}} V_{\text{o}}
\end{align}
$$
```

from the ideal value $K$ by the two load factors $k_{\text{i}}$ and $k_{\text{o}}$. The reduction in gain is avoided if the two factors equal unity, that is, if $z_{\text{i}} = \infty$ and $z_{\text{o}} = 0$. Thus, in addition to the required gain $K$, a good amplifier has a very large input impedance $z_{\text{i}}$ and a very small output impedance $z_{\text{o}}$. See GAIN.

The operational amplifier (op amp) is a commonly used general-purpose amplifier. It is implemented as an integrated circuit on a semiconductor chip, and functions as a voltage amplifier whose essential characteristics at low frequencies are very high voltage amplification, very high input resistance, and very low output resistance. See INTEGRATED CIRCUITS.

The transconductance amplifier has become widely used. In contrast to operational amplifiers, which convert an input voltage to an output voltage, transconductors are voltage-to-current converters described by the transconductance parameter $g_{\text{m}}$, which satisfies Eq. (3). Thus, the output current $I_{\text{out}}$ is proportional to the input voltage $V_{\text{in}}$.

```
$$I_{\text{out}} = g_{\text{m}} V_{\text{in}}$$
```

As do operational amplifiers, ideal transconductors have an infinite input resistance, but they also have an infinite output resistance so that the output is an ideal current source. One of the attractive properties of transconductance amplifiers is their wide bandwidth. Very simple transconductance circuits can be designed which maintain their nominal $g_{\text{m}}$ values over bandwidths of several hundred megahertz, whereas operational amplifiers often have high gain only over a frequency range of less than 100 hz, after which the gain falls off rapidly. Consequently, in high-frequency communications applications, circuits built with transconductance amplifiers generally give much better performance than those with operational amplifiers.

Typically, amplifiers increase the power or signal levels from low-power sources, such as microphones, strain gages, magnetic disks, or antennas. After the small signals have been amplified, the amplifier’s output stage must deliver the amplified signal efficiently, with minimal loss, and with no distortion to a load, such as a loudspeaker.

# Amplitude (wave motion)

The maximum magnitude (value without regard to sign) of the disturbance of a wave. The term “disturbance” refers to that property of a wave which perturbs or alters its surroundings. It may mean, for example, the displacement of mechanical waves, the pressure variations of a sound wave, or the electric or magnetic field of light waves. Sometimes in older texts the word amplitude is used for the disturbance itself; in that case, amplitude as meant there is called peak amplitude. This is no longer common usage.

If the medium which a wave disturbs dissipates the wave by some nonlinear behavior or other means, the amplitude will, in general, depend upon position. See DISPLACEMENT (MECHANICS); LIGHT; SOUND; WAVE MOTION.

# Amplitude modulation

The process or result of the process whereby the amplitude of a carrier wave is changed in accordance with a modulating wave. This broad definition includes applications using sinusoidal carriers, pulse carriers, or any other form of carrier; the amplitude factor of which changes in accordance with the modulating wave in any unique manner. See MODULATION.

Practical examples of amplitude modulation (AM) include AM radio broadcasting, single-sideband transmission systems, vestigial-sideband systems, frequency-division multiplexing, time-division multiplexing, phase-division multiplexing, and reduced-modulation systems. See MULTIPLEXING; SINGLE-SIDEBAND.

Amplitude modulation is also defined in a more restrictive sense to mean modulation in which the amplitude factor of a sine-wave carrier is linearly proportional to the modulating wave. AM radio broadcasting is a familiar example. At the radio transmitter the modulating wave is the audio-frequency program signal to be communicated; the modulated wave that is broadcast is a radio-frequency, amplitude-modulated sinusoid. See AMPLITUDE-MODULATION RADIO.

In AM the modulated wave is composed of the transmitted carrier, which conveys no information, plus the upper and lower sidebands, which (assuming the carrier frequency exceeds twice the top audio frequency) convey identical and therefore mutually redundant information. J. R. Carson in 1915 was the first to recognize that, under these conditions and assuming adequate knowledge of the carrier, either sideband alone would uniquely define the message. This eventually led to the development of single-sideband (SSB) and vestigial-sideband (VSB) modulation. Apart from a scale factor, the spectrum of the upper sideband and lower sideband is the spectrum of the modulating wave displaced, respectively, without and with inversion by an amount equal to the carrier frequency. See AMPLITUDE-MODULATION DETECTOR; AMPLITUDE MODULATOR; FREQUENCY-MODULATION DETECTOR; FREQUENCY MODULATION.

# Amplitude-modulation detector

A device for recovering information from an amplitude-modulated (AM) electrical signal. Such a signal is received, usually at radio frequency, with information impressed in one of several ways. The carrier signal may be modulated by the information signal as double-sideband (DSB) suppressed-carrier (DSSC or DSBSC), double-sideband transmitted-carrier (DSTC or DSBTC), single-sideband suppressed-carrier (SSBSC or SSB), vestigial sideband (VSB), or quadrature-amplitude modulation (QAM).

The field of amplitude-modulation detector requirements splits by application, complexity, and cost into the two categories of synchronous and asynchronous detection. An analog implementation of nonlinear synchronous detection, which is typically carried out with a diode circuit, is favored for consumer applications, AM-broadcast radio receivers, minimum-cost products, and less critical performance requirements. Synchronous detectors, in which the received signal is multiplied by a replica of the carrier signal, are implemented directly according to their mathematics and block diagrams, and the same general detector for satisfies the detection requirements of all SSB, DSB, and VSB signals. Although synchronous detectors may operate in the analog domain by using integrated circuits, more commonly digital circuits are used because of cost, performance, reliability, and power advantages.

In synchronous detection there are two conceptual approaches: to reverse the modulation process (which is rather difficult), or to remodulate the signal from the passband (at or near the transmitter’s carrier frequency) to the baseband (centered at dc or zero frequency). The remodulation approach is routine. Unfortunately, a nearly exact replica of the transmitter’s