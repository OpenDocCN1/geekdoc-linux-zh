
people in different situations. Understanding noise and its control requires a knowledge of the major source of noise, its propagation, human response to noise, and the physics of methods of controlling noise. The continuing increase in noise levels from many different human activities in industrialized societies has led to the term noise pollution.

Noise as an unwanted by-product of an industrialized society affects not only the operators of machines and vehicles, but also other occupants of buildings in which machines are installed, passengers of vehicles, and most importantly the communities in which machines, factories, and vehicles are operated. [M.J.Cr.]

## Acoustic radiation pressure

The net pressure exerted on a surface or interface by an acoustic wave. One might presume that the back-and-forth oscillation of fluid caused by the passage of an acoustic wave will not exert any net force on an object, and this is true for sound waves normally encountered. Intense sound waves, however, can exert net forces in one direction of sufficient magnitude (proportional to the sound intensity) to balance gravitational forces and thus levitate an object in air.

Forces due to acoustic radiation pressure have been used to calibrate acoustic transmitters, to deform and break up liquids, to collect like objects, to separate particles (including biological cells) based on mechanical properties, and to position objects in a sound field, sometimes levitating the sample so that independent studies of the object’s properties can be performed. Single bubble sonoluminescence phenomena depend on acoustic radiation forces to maintain a bubble in a zone while its substantial radial oscillations take place. See ACOUSTIC LEVITATION; SONOCHEMISTRY; ULTRASONICS. [R.E.A]

## Acoustic radiometer

A device to measure the acoustic power or intensity of a sound beam by means of the force or torque that the beam exerts on an inserted object or interface. The underlying theory involves the concept of radiation pressure. Such pressure occurs, for example, when a plane sound wave is partially reflected at an interface between two materials, with the nonlinear interaction between the incident and reflected waves giving rise to a steady pressure on the interface. If a narrow beam is incident on the interface and the transmitted wave is fully absorbed by the second material, the magnitude of the radiation force F (area integral of radiation pressure) equals a constant times W/c, where W is the power of the sound beam and c is the sound speed.

A modern acoustic radiometer, used to measure the total power of an ultrasonic sound beam in water and other liquids, employs a vane suspended in the fluid in such a manner that its displacement in a direction normal to its face is proportional to the net force pushing on its front face. The vane is ideally of dimensions somewhat larger than the incident beam’s diameter, so that the encountered force is associated with the entire incident beam. To eliminate the possibility of sound being reflected toward the transmitting transducer, the vane is oriented at 45° to the incident sound beam. The vane’s horizontal displacement is made to be proportional to the imposed force by fastening the vane at one end of a long pendulum whose rotation from the vertical is opposed by the effect of gravity, such that the apparent spring constant for displacement in a direction at 45° to the face is approximately Mg/L, where M is the apparent mass of the vane (corrected for the presence of water), g is the acceleration of gravity, and L is the length of the pendulum. A nonlinear acoustics theory for such a circumstance yields a proportionality relation between the net horizontal radiation force on the vane and the acoustic power associated with the incident beam. Because the deflection of the vane is proportional to the radiation force, the acoustic power can be determined. See BUOYANCY; PENDULUM.

The concept of the vane device evolved from that of the Rayleigh disk, which was a circular disk that could rotate about its diameter and whose deflection from a nominal 45° orientation was opposed by a torsional spring. The Rayleigh disk was taken to have a radius much smaller than the wavelength, and its use ideally yielded a measurement of the local acoustic intensity that would have existed at the center of the disk were the disk not present. See ACOUSTIC RADIATION PRESSURE; SOUND; SOUND INTENSITY; SOUND PRESSURE. [A.D.P.; S.M.]

## Acoustic resonator

A device consisting of a combination of elements having mass and compliance whose acoustical reactances cancel at a given frequency. Resonators are often used as a means of eliminating an undesirable frequency component in an acoustical system. In other instances resonators are used to produce an increase in the sound pressure in an acoustical field at a particular frequency.

Resonators are useful most often in the control of low-frequency sound. They are of particular value in reducing the noise from sources having constant frequency excitation. Resonators have also found considerable application in architectural acoustics. It is often difficult to obtain adequate control of reverberation time at low frequencies in a large studio or auditorium using conventional acoustical materials. A number of designs for these spaces have included the construction of resonators behind walls or in the ceiling to obtain increased low-frequency absorption and thus provide more satisfactory reverberation characteristics. See ARCHITECTURAL ACOUSTICS.

![](img/2cf7974cd6027baa297e5cd95d3d6d43_26_0.png)

The Helmholtz resonator (see illustration) is the simplest and most often utilized acoustical resonator. The unit consists of a straight tube of length L and cross-sectional area S, connected to a closed volume V. This combination is directly analogous to the simple series LC electrical circuit. See ACOUSTIC IMPEDANCE; MÜLLER. [W.J.G.]

## Acoustic signal processing

A discipline that deals generally with the extraction of information from acoustic signals in the presence of noise and uncertainty. Acoustic signal processing has expanded from the improvement of music and speech sounds and a tool to search for oil and submarines to include medical instrumentation; techniques for efficient transmission, storage, and presentation of music and speech; and machine speech recognition. Undersea processing has expanded to study and underwater weather and long-term global ocean temperature changes, mammal tracking at long ranges, and monitoring of hot vents. These techniques stem from the rapid advances in computer science, especially the development of large, inexpensive memories and ever-increasing processing speeds.

Sound can be said to be low and slow compared to computers. The audio frequencies are low, spanning roughly the range from 15 to 25,000 hertz, with seismic frequencies below this range and frequencies relevant to medical ultrasonics above. All of these frequencies are well within the limits of analog-to-digital input samplers and digital-to-analog output converters that form the bridges between continuous-time physical waveforms and the streams of digits handled by a computer. The speed of sound in water, compared to light and radio waves at 3 × 10⁸ m/s (10⁹ ft/s), is the upper limit for electrical signals in computer circuits. A computer can carry out thousands of elementary computations between input samples. See ANALOG-TO-DIGITAL CONVERTER; DIGITAL-TO-ANALOG CONVERTER; SOUND.

Signal processors "think" in two domains. One domain is the picture or waveform s(t) and the other is how it changes in time. This time-domain picture is s(t); in time, and s might be the sound pressure or a microphone voltage. The other picture is the complex magnitude at every important frequency during an interval of time. This frequency-domain or spectrum picture is S(f, Tₙ); f is the frequency in hertz, and Tₙ is the nth time interval. J. Fourier (1768–1830) formulated his series version of this picture and showed that s(t) could be calculated from S(f), and vice versa. Mathematicians have developed other versions of spectral transforms, each with its special area of application. See FOURIER SERIES AND TRANSFORMS; INTEGRAL TRANSFORM.

Each domain picture provides the same information, but sometimes it is easier to think, or compute, using one domain rather than the other. The computer version uses the DFT (discrete Fourier transform). Transformers were formerly time-consuming computations: For N points in one domain the time needed was proportional to N squared. In the 1960s a layered algorithm was developed to speed up the DFT. The emphasis is on simple sizes which are integer powers of 2. These fast Fourier transforms have had a major impact on spectral processing.

One example of acoustic signal processing for biomedical purposes is its use in restoring hearing. The cochlea in the inner ear is nature's time-domain-to-frequency-domain transformer, exciting a line of nerve endings in response to something like the short-time spectrum of the input. For people in whom this natural mechanism is dysfunctional but the cochlear nerve is intact, a technology is developing based on modest DFT analysis of sound near an ear, feeding perhaps 32 channels to an implanted microconnector in the cochlear nerve bundle. See HEARING (HUMAN); HEARING AID; PHYSIOLOGICAL ACOUSTICS.

One of the most difficult signal processing areas is machine recognition of spoken speech. Vocabulary size and number of speakers are key parameters. The fundamental problems are:
- words are not spoken separately, but in streams of connected speech,
- a phrase is seldom said the same way every time,
- the vocabulary is enormous, and
- there is a huge number of speaker accents and rhythms.
The signal processing must segment an utterance into phonemes, words, or phrases; pick out key features; or compare the whole segment with a library for likely matches.

(T.G.Bi.)

## Acoustic torpedo

An autonomous undersea vehicle that can be launched from submarines, surface ships, or aircraft to attack enemy submarines and surface ships. Its main components are a guidance and control system, a power plant to provide propulsive and electrical energy, a propulsor to control speed and direction, and a warhead. The launching platform performs the function of determining the approximate location of the target and launching the torpedo in the proper direction. The torpedo typically utilizes an acoustic sensor in its nose and is controlled by an on-board computer. During its operation, the torpedo searches the volume of the ocean determined by the launch platform. It progresses through the following stages: detection (an object is present), classification (the object is a target of interest), homing (aimed at the object), and detonation of the warhead. See GUIDANCE SYSTEMS; HOMING.

(F.W.Sj.)

## Acoustics

The science of sound, which in its most general form endeavors to describe and interpret the phenomena associated with motional disturbances from equilibrium of elastic media. An elastic medium is one such that if any part of it is displaced from its original position with respect to the rest, as for example by an impact, it will return to its original position and the disturbing influence is removed. Acoustics was originally limited to the human experience produced by the stimulation of the human ear by sound incident from the surrounding air. Modern acoustics, however, deals with all sorts of sounds which have no relation to the human ear, for example, seismological disturbances and ultrasonics.

Basic acoustics may be divided into three branches, namely, production, transmission, and detection of sound. Any change of stress or pressure producing a local change in density or a local displacement from equilibrium in an elastic medium can serve as a source of sound. Transmission of sound takes place through an elastic medium by means of wave motion. The most important sound waves are harmonic waves, defined as waves for which the propagated disturbance at any point in its path varies sinusoidally with time with a definite frequency or number of complete cycles per second (the unit being the hertz). Acoustics deals with waves of all frequencies, but not all frequencies are audible by human beings, for whom the average range of audibility extends from 20 to 20,000 Hz. Sound below 20 Hz is referred to as infrasonic, and that above 20,000 Hz is called ultrasonic.

The detection of sound is made possible by the incidence of transmitted sound energy on an appropriate acoustic transducer, such as the ear. For modern applied acoustics, transducers such as the microphone, based on the piezoelectric effect, are widely used. Generally speaking, any transducer used as a source of sound is also available as a detector, though the sensitivity varies considerably with the type.

(R.Bi.)

## Acousto-optics

The field of science and technology that is concerned with the diffraction of visible or infrared light (usually from a laser) by high-frequency sound in the frequency range of 50–2000 MHz. The term “acousto” is a historical misnomer; sound in this frequency range should properly be called ultrasound. Such sound cannot be supported by air; but propagates as a mechanical wave disturbance in amorphous or crystalline solids, with a sound velocity ranging from 0.6 to 6 km/s (0.4 to 4 mi/s), and a wavelength from 3 to 100 µm. See LASER; ULTRASONICS.

The sound wave causes a displacement of the solid's molecules either in the direction of propagation (longitudinal wave) or perpendicular to it (shear waves). In either case, it sets up a corresponding wave of refractive-index variation through local dilatation or distortion of the solid medium. It is this wave that diffracts the light by acting as a three-dimensional grating, analogous to x-diffraction in crystals. The fact that the grating is moving is responsible for shifting the frequency of the diffracted light through the Doppler effect. See DIFFRACTION GRATING; DOPPLER EFFECT; REFRACTION OF WAVES; WAVE MOTION; X-RAY DIFFRACTION.

Since the 1960s, acousto-optics has moved from a scientific curiosity to a relevant technology. This evolution was initially driven by the need for fast modulation and deflection of light beams, and later by demands for more general optical processing. It was made possible by the invention of lasers, the development of efficient ultrasonic transducers, and the formulation of realistic models of sound-light interaction. See TRANSFORMATION.

(A.K.)

## Acquired immune deficiency syndrome (AIDS)

A viral disease of humans caused by the human immunodeficiency virus (HIV), which attacks and compromises the body's immune system. Individuals infected with HIV progress through a spectrum of stages that ultimately lead to the critical end point, acquired immune deficiency syndrome. The disease is characterized by a profound progressive irreversible depletion of T-helper-inducer lymphocytes (CD4+ lymphocytes), which leads to the onset of multiple and recurrent opportunistic infections by other viruses, fungi, bacteria, and protozoa, as well
