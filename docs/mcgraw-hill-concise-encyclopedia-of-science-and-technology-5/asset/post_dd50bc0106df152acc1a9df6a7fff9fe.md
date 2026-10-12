
## Pulse modulator
samples. One of these serves as a synchronizing marker that indicates the beginning of each 192-pulse sequence, while the other 192 pulses are the composite of 8 pulses from each of 24 voice signals, with each 8-pulse sequence occupying a specified position. T1 carriers and similar types of digital carrier systems are in widespread use in the world’s telephone networks.

### Bandwidth requirements
Pulse modulation systems may incur a significant bandwidth penalty compared to the transmission of a signal in its analog form. An example is the standard PCM transmission of an analog voice signal band-limited to 4000 hertz over a T1 carrier. Here the sampling, quantizing, and coding process produces 8 binary pulses 8000 times per second for a total of 64,000 binary pulses per second; the pulses occur every 15.625 microseconds. Depending on the shape of the pulses and the amount of intersymbol interference, the required transmission bandwidth will fall in the range of 32 000 to 64,000 hertz. This compares to a bandwidth of only 4000 hertz for the transmission of the signal in analog mode.

### Applications
PAM, PWM, and PPM found significant application early in the development of digital communications, largely in the domain of radio telemetry for remote monitoring and sensing. They have since fallen into disuse in favor of PCM. Since the early 1960s, many of the world’s telephone network providers have gradually, and by now almost completely, converted their transmission facilities to PCM technology. The bulk of these transmission systems use some form of time-division multiplexing, as exemplified by the 24-voice channel T1 carrier structure. These carrier systems are implemented over many types of transmission media, including twisted pairs of telephone wiring, coaxial cables, fibrtic cables, and microwave. See **COAXIAL CABLE; COMMUNICATIONS CABLE; MICROWAVE; OPTICAL COMMUNICATIONS; OPTICAL FIBERS; SWITCHING SYSTEMS (COMMUNICATIONS); TELEPHONE SERVICE.**

The deployment of high-speed networks such as the Integrated Digital Network (ISDN) in many parts of the world has also relied heavily on PCM technology. PCM and various modified forms such as delta modulation (DM) and adaptive differential pulse-code modulation (ADPCM) have also found significant application in satellite transmission systems. See **COMMUNICATIONS SATELLITE; DATA COMMUNICATIONS; ELECTRICAL COMMUNICATIONS; INTEGRATED SERVICES DIGITAL NETWORK (ISDN); MODULATION.** [H.J.H.]

## Pulse modulator
A device for the pulse modulation of a radio-frequency carrier signal. In pulse modulation, information is transmitted by generating a train of discrete pulses whose amplitude, duration, position, or even presence is controlled in accordance with the signal. See **PULSE MODULATION.**

### Pulse-amplitude modulation
In pulse-amplitude modulation (PAM) the desired signal to be transmitted is sampled periodically (Fig. 1). PAM may be accomplished by the use of a multiplier circuit. The signal that contains the intelligence to be transmitted is applied to one of the multiplier inputs, and the train of pulses known as the sampling signal is applied to the other multiplier input. If this train of pulses has an amplitude of one during the pulse and zero elsewhere, the multiplier output will consist of a train of pulses, each having an amplitude equal to the signal amplitude at the time of sampling (Fig. 1). The main reason for using PAM is that several signals may be transmitted over a single communication channel by a technique known as multiplexing. See **MULTIPLEXING AND MULTIPLE ACCESS.**

The most simple technique for multiplexing several signals onto a single channel is to use a rotating multipole switch known as an commutator. The commutator may serve as the sampler, or modulator, as well as the multiplier. A commutator must be used on the receiving end as well as the transmitting end of the multiplexed channel in order to unscribe the signals. These commutators must be synchronized so that each message is sent to its proper destination at the receiving end. For example, several telephone conversations might be sampled and multiplexed onto a single telephone line. An easily identifiable synchronizing signal must be sent to synchronize the commutators at the two ends of the system. A low-pass filter is used in each message line at the receiving end to pass only the desired message frequencies and remove the higher frequencies of the pulses. See **ELECTRIC FILTER.**

### Pulse-width and pulse-position modulation
PAM is a satisfactory method of communication when transmission distances are short enough to maintain high signal-to-noise ratios. However, when transmission distances become long, such as many miles, the atmospheric noise from lightning and other electrical noise that is induced into either a hard-wire line or a radio antenna may degrade the signal-to-noise ratio sufficiently so at least cause annoyance and at worst render the message unintelligible. Both pulse-width modulation (PWM) and pulse-position modulation (PPM) have been used in the past with the hope of improving the signal-to-noise ratio. See **ELECTRICAL INTERFERENCE; ELECTRICAL NOISE; SIGNAL-TO-NOISE RATIO.**

PWM may be obtained from the PAM pulse by charging a small capacitor to the peak voltage of each pulse as it comes along, and then discharging the capacitor through a constant current source before the next pulse arrives. Then a capacitor voltage decreases linearly to zero during a time that is proportional to the pulse amplitude. These triangular pulses may then be passed through a Schmitt trigger circuit to square them up and provide constant amplitude pulses of varying width.

PPM may then be obtained by differentiating the PWM signals to produce narrow pulses at both the leading and trailing edges of the PWM pulses. The leading-edge pulse is used as the reference pulse, and the time difference between it and the trailing-edge pulse represents the modulation amplitude. These sharp PPM pulses may be squared up by the use of either a Schmitt trigger circuit or a one-shot multiplier circuit. Both the PPM and PWM signals are subject to noise modulation so their use may or may not improve the signal-to-noise ratio in comparison with a PAM system. See **MULTIVIBRATOR.**

### Pulse-code modulation
A signal transmission system of any type may become essentially immune to atmospheric and other induced noise when pulse-code modulation (PCM) is used. In this type of modulation, the modulating signal is first sampled (Fig. 2a). The resulting PAM signals are then quantized by a circuit that compares each pulse amplitude with a set of predetermined levels and produces a stepwise-varying replica of the original signal having only the predetermined voltage levels. In Fig. 2b, eight equally spaced levels were chosen to represent signals limited to the range from approximately 0 to 7 V peak amplitude. Thus the quantizing levels are separated by 1 V. Each quantized level is then represented by a sequence of 8 pulses known as a code. Any of many different coding systems may be used, but the binary code is basic and is very commonly used (Fig. 2c). Analog-to-digital converters are available in integrated-circuit form. See **ANALOG-TO-DIGITAL CONVERTER; INTEGRATED CIRCUITS.**

If the transmission path is very long, one or more repeater stations may be needed at intermediate points. These repeaters receive the signal while it is still larger than the noise, remove the noise, amplify the signal, and retransmit it along the channel.

![](img/2cf7974cd6027baa297e5cd95d3d6d43_1818_0.png)

![](img/2cf7974cd6027baa297e5cd95d3d6d43_1819_0.png)

Fig. 2. Pulse-code modulation. *(a)* Signal sampling. *(b)* Quantization. *(c)* Binary pulse coding.

In fact, PCM signals that are weaker than the noise may be received and the noise rejected if a phase-locked loop is used as the demodulator in the receiver. See **PHASE-LOCKED LOOPS**. The signal-to-noise ratio of PCM voice communication decreases if the signal level decreases significantly from its maximum permissible value because some of the quantization levels are then not used. In order to overcome this problem, signal compression is used prior to modulation. This compression is accomplished by amplifying the weak signals more than the strong ones so the variation in signal level is greatly reduced. In order to restore the original relative signal levels at the receiving end of the system after demodulation, a circuit known as an expander is used to amplify the stronger signals more than the weak ones. A circuit that will serve as either a compressor or expander is known as a compander. [C.L.A.]

## Pumice
A rock froth, formed by the extreme puffing up of liquid lava by expanding gases liberated from solution in the lava prior to and during solidification. Some varieties will float in water for many weeks before becoming waterlogged. Typical pumice is siliceous (rhyolite or dacite) in composition, but the lightest and most vesicular pumice (known also as reticulate and thread-lace scoria) is of basaltic composition. See **LAVA; VOLCANIC GLASS**. [G.A.M.]

## Pump
A machine that draws a fluid into itself through an entrance port and forces the fluid out through an exhaust port (see illustration). A pump may serve to move liquid, as in a cross-country pipeline; to lift liquid, as from a well or to the top of a tall building; or to put fluid under pressure, as in a hydraulic brake. These applications depend predominantly upon the discharge

![](img/2cf7974cd6027baa297e5cd95d3d6d43_1819_1.png)

Pumps. *(a)* Reciprocating. *(b)* Rotary. *(c)* Centrifugal.

characteristic of the pump. A pump may also serve to empty a container, as in a vacuum pump or a sump pump, in which case the application depends primarily on its intake characteristic. See **CENTRIFUGAL PUMP; COMPRESSOR; DISPLACEMENT PUMP; FAN; FUEL PUMP; PUMPING MACHINERY; VACUUM PUMP**. [E.F.W.]

## Pumped storage
A process, also known as hydroelectric storage, for converting large quantities of electrical energy to potential energy by pumping water to a higher elevation, where it can be stored indefinitely and then released to pass through hydraulic turbines and generate electrical energy. An indirect process is necessary because electrical energy cannot be stored effectively in large quantities. Storage is desirable, as the consumption of electricity is highly variable between day and night, between weekday and weekend, as well as among seasons. Consequently, much of the generating equipment needed to meet the greatest daytime load is unused or lightly loaded at night or on weekends. During those times the excess capability can be used to generate energy for pumping, hence the necessity for storage.

A typical pumped-storage development is composed of two reservoirs of essentially equal volume situated to maximize the difference in their levels. These reservoirs are connected by a system of waterways along which a pumping-generating station is located (see illustration). Under favorable geological conditions,

![](img/2cf7974cd6027baa297e5cd95d3d6d43_1819_2.png)

the station will be located underground; otherwise it will be situated on the lower reservoir. The principal equipment of the station is the pumping-generating unit. In United States practice, the machinery is reversible and is used for both pumping and generating; it is designed to function as a motor and pump in one direction of rotation and as a turbine and generator in opposite rotation. See **ELECTRIC POWER GENERATION; PUMPING MACHINERY; WATERPOWER**. [D.L.G.]

## Pumping machinery
Devices which convey fluids, chiefly liquids, from a lower to a higher elevation or from a region of lower pressure to one of higher pressure. Pumping machinery may be broadly classified as mechanical or as electromagnetic. In mechanical pumps, the fluid is conveyed by direct contact with a moving part of the pumping machinery. The two basic types are
- (1) velocity machines, centrifugal or turbine pumps, which impart energy to the fluid primarily by increasing its velocity, then converting part of this energy into pressure or head, and
- (2) displacement machines with plungers, pistons, cams, or other confining forms which act directly on the fluid, forcing it to flow against a higher pressure.

See **CENTRIFUGAL PUMP; DISPLACEMENT PUMP**.

Where direct contact between the fluid and the pumping machinery is undesirable, as in atomic energy power plants for circulating liquid metals used as reactor coolants or as solvents
