
RADIATION PRESSURE; BIOMEDICAL ULTRASONICS; NONDESTRUCTIVE EVALUATION; SHOCK WAVE; SOUND WAVE; TURBULENCE

The principal feature that distinguishes nonlinear acoustics from nonlinear optics is that most acoustic media exhibit only weak dispersion, whereas media in which nonlinear optical effects arise exhibit strong dispersion. Dispersion is the dependence of propagation speed on frequency. In optical media, strong nonlinear wave interactions require that phase-matching conditions be satisfied, which can be accomplished only for several frequency components at one time. In contrast, all frequency components in a sound wave propagate at the same speed and are automatically phase-matched, which permits strong nonlinear interactions to occur among all components in the frequency spectrum. See NONLINEAR OPTICS.

Acoustic streaming is a nonlinear effect because the velocity of the flow depends quadratically on the amplitude of the sound, and the flow is not predicted by linear theory. Absorption due to viscosity and heat conduction results in a transfer of momentum from the sound field to the fluid. This momentum transfer manifests itself as steady fluid flow.

Acoustic streaming produced in sound beams is enhanced considerably when shocks develop. Shock formation generates a frequency spectrum rich in higher harmonics. Because thermal absorption increases quadratically with frequency, attenuation of the wave, and therefore the streaming velocity, increases markedly following shock formation. Streaming is also generated in acoustic boundary layers formed by standing waves in contact with surfaces. Measurements of acoustic streaming have been used to determine the bulk viscosity coefficients of fluids. Thermoacoustic engines are refrigerators adversely affected by heat transport associated with streaming. See THERMOACOUSTICS.

Phase conjugation refers to waveform reversal, also called time reversal, at a single frequency. The latter terminologies more clearly describe this procedure. A waveform is captured by a phase conjugation device and reversed in such a way that it propagates backward to the source in the same way that it was originally toward the conjugator. Sound that is radiated from a point source and propagates through an inhomogeneous medium that introduces phase distortion in the wave field is thus retransmitted by the conjugator in such a way as to compensate for the phase distortion and to focus the wave back on the point source.

Phase conjugation is used to compensate for phase distortion in applications involving imaging and targeting of waves on surfaces. The most successful techniques for acoustical phase conjugation are based on modulation of acoustical properties of a material that captures the incident sound wave. The modulation is twice the frequency of the incident sound wave, and it is induced by an electric field applied to piezoelectric material, or a magnetic field applied to magnetostrictive material. Often the modulated property of interest is the sound speed in the material. When the incident wave at frequency $f$ propagates through a medium in which the sound speed fluctuates at frequency $2f$, parametric interaction generates a wave at the difference frequency $f$ that propagates backward as though reversed in time. See MAGNETOSTRICTION; OPTICAL PHASE CONJUGATION; PIEZOELECTRICITY.

Phenomena associated with nonlinear acoustics have proved useful in both diagnostic and therapeutic applications of biomedical ultrasound. A very significant breakthrough in diagnostic imaging, especially for echocardiography and abdominal ultrasound imaging, is based on second-harmonic generation. Medical ultrasound imaging is performed at frequencies of several megahertz. Images constructed from the backscattered second-harmonic component have substantially reduced clutter and have been affected by the propagation of ultrasound through the outer layers of skin, which is the primary cause of phase aberrations. In another technique, microbubbles are injected into the bloodstream to enhance echoes backscattered from blood flow. The microbubbles are fabricated to make them resonant at diagnostic imaging frequencies, and they become strongly nonlinear oscillators when excited by ultrasound. Imaging is based on echoes at harmonics of the transmitted signal. Frequencies backscattered from the microbubbles differ from those in echoes coming from the surrounding tissue, which highlights the locations of the microbubbles and therefore of the blood flow itself.

A notable therapeutic application is lithotripsy, which refers to the noninvasive disintegration of kidney stones and gallstones with focused shock waves. Nonlinear acoustical effects in lithotripsy are associated not only with the propagation of the shock wave but also with the generation of cavitation activity near the stones. Radiation of shock waves due to the collapse of cavitation bubbles is believed to be the dominant cause of stone breakup. An emerging therapeutic application, high-intensity focused ultrasound (HIFU), utilizes the heat deposited by shock waves that develop in beams of focused ultrasound. The heating is so intense and localized that the potential exists for precise ablation of scar tissue, cauterization of internal organs, and removal of tumors.

## Nonlinear control theory

A control system involves a plant and a controller. Plants are objects as diverse as a satellite, a distillation column, a robot arm, and a colony of bacteria. After measuring actual outputs of the plant, the controller computes signals that are applied at the inputs to the plant to achieve desired outputs. The design of controllers must be based upon mathematical models of plants, which in most realistic situations are composed of nonlinear differential and difference equations. A standard approach is to linearize the equations and use the powerful methods available for the design of linear control systems. See DIFFERENTIAL EQUATION; LINEAR SYSTEM ANALYSIS; OPTIMAL CONTROL (LINEAR SYSTEMS).

When the controlled outputs are allowed to have large deviations from the desired steady-state values, a linearized model will cease to describe the plant accurately, thereby causing erroneous results in the design. Linearized design models also fail in those important situations where nonlinearities are introduced into a controller to achieve a desired performance, generally at reduced cost. Typical examples of nonlinear controllers are on-off relays for temperature regulation in heating and cooling systems, switching elements in robot manipulators, and jet thrusters for the attitude control of space vehicles.

Unlike linear systems, there is no general theory for nonlinear systems. Nonlinear control theory is fragmented into areas centered around those classes of systems that are most prominent in applications.

A simple nonlinear control system is the inverted pendulum (illus. *a*), where it is required to keep the pendulum in an upright position by applying the torque $u(t)$ at its base. The pendulum can be considered as a generic model for a rocket booster balanced on top of a gimbaled thruster engine (illus. *b*), and a controlled robot arm (illus. *c*). Newton's second law of motion for the pendulum is Eq. (1), where $m(t)$ is the mass of the bob,

$$m\ddot{\theta}(t)=\frac{m g}{L}\sin(\theta(t))$$

(1)

$\ell$ is the length of the pendulum, and $g$ is the acceleration due to gravity. By choosing the angular position $\theta=x_1$ and angular velocity $\dot{\theta}=x_2$ of the bob as the state of the system, Eq. (1) can be rewritten as two first-order state equations (2).

$$
\begin{array}{l} 
\dot{x}_1=x_2 \\ 
\dot{x}_2=\frac{g}{\ell}\sin x_1+u 
\end{array}
$$

(2)

See PENDULUM.

![](img/2cf7974cd6027baa297e5cd95d3d6d43_1504_0.png)

Nonlinear systems. (*a*) Inverted pendulum, which serves as a model for (*b*) a rocket booster and (*c*) a robot arm.

If the torque is absent ($u=0$), the upright position of a motionless pendulum ($x_1=0$, $x_2=0$) is an equilibrium state: $x_1=0$, $x_2=0$. If the pendulum is slightly perturbed at this state, it will fall down and keep oscillating around the other equilibrium point at $x_1=\pi$ and $x_2=0$. To keep the pendulum in the upright position in physically realistic situations involving perturbations, the torque $u$ is chosen to be a suitable function $\phi$ of the state $x_1$, $x_2$, as in Eq. (3).

$$u=\phi(x_1,x_2)$$

(3)

$u$ should be a feedback control law in terms of the state is one of the most important results of control theory. [D.D.S.]

## Nonlinear optical devices

Devices that use the fact that the polarization in any real medium is a nonlinear function of the optical field strength to implement various useful functions. The nonlinearities themselves can be grouped roughly into second-order and third-order. Materials that possess inversion symmetry typically exhibit only third-order nonlinearities, whereas materials without inversion symmetry can exhibit both second- and third-order nonlinearities. See CRYSTALLOGRAPHY; ELECTRIC SUSCEPTIBILITY; ELECTROMAGNETIC RADIATION; POLARIZATION OF DIELECTRICS.

### Second-order devices

Devices based on the second-order nonlinearity involve three-photon (or three-wave) mixing. In this process, two photons are mixed together to create a third photon, subject to energy- and momentum-conservation constraints. Different names are ascribed to this mixing process, depending upon the relative magnitudes of the energies of the participating photons. See CONSERVATION OF ENERGY; CONSERVATION OF MOMENTUM. When the two beginning photons are of equal energy or frequency, the mixing process gives a single photon with twice the energy or frequency of the original one. This mixing process is called second-harmonic generation. Second-harmonic generation is used in devices where photons of visible frequency are desired but the available underlying laser system is capable of producing only infrared photons. For example, the neodymium-doped yttrium-aluminum-garnet (Nd:YAG) laser produces photons in the infrared with a wavelength of 1.06 micrometers. These photons are mixed in a crystal with a large second-order nonlinearity and proper momentum-conservation characteristics to yield green second-harmonic photons of 0.532-$\mu$m wavelength. Under different momentum-conservation constraints, a similar interaction can take place between two photons of different frequency, resulting in photons whose energy or frequency is the sum of those of the original photons. This process is called sum-frequency mixing. See LASER.

Optical parametric oscillation/amplification occurs when one of the two initial photons has the largest energy and frequency of the three. A high-energy photon and a low-energy photon mix to give a third photon with an energy equal to the difference between the two initial photons. If initially the third field amplitude is zero, it is possible to generate a third field from nothing; in this case the process is called optical parametric oscillation. If the third field exists but at a low level, it can be amplified through the optical parametric amplification process. See PARAMETRIC AMPLIFIER.

### Third-order devices

Devices based on the third-order nonlinearity involve a process called four-photon (or four-wave) mixing. In this process, three photons are mixed together to create a fourth photon, subject to energy- and momentum-conservation constraints. The four-photon mixing nonlinearity is responsible for the existence of so-called self-action effects where the refractive index and absorption coefficient of the medium are modified by the light field's own presence. This also accounts for third-harmonic generation and related processes, as well as phase-conjugation processes.

In a medium with a third-order nonlinearity, the refractive index and absorption coefficient of a light field present in the medium are modified by the strength of the light intensity. Because the field effectively acts on itself, this interaction is termed a self-action effect. The momentum-conservation constraints are automatically satisfied because of the degenerate frequencies involved in the interaction. Such an interaction manifests itself by changing the total absorption experienced by the light field as well as by changing the velocity of propagation of the light field. See ABSORPTION OF ELECTROMAGNETIC RADIATION; REFRACTION OF WAVES.

There are many devices based on the self-action effects. A reverse saturable absorber becomes more opaque because of the nonlinear absorption (also called two-photon absorption) that it manifests. Refractive-index changes can be used to change the transmission characteristics of resonant cavities and other structures by modifying the effective optical path length (the product of actual structure length times the effective refractive index for the structure) and shifting the cavity resonances to other frequencies. Several nonlinear optical switches have been proposed based upon this resonance-shifting phenomenon. See CAVITY RESONATOR; OPTICAL STABILITY.

In a third-harmonic generation process, three photons of like energy and frequency are mixed to yield a single photon with three times the energy and frequency of the initial photons. Applications of third-harmonic generation are typical in the areas of frequency conversion.

Phase-conjugation devices make use of a property that third-order media possess whereby energy- and frequency-degenerate photons from two counterpropagating fields are mixed with an incoming photon to yield a photon with exactly the opposite propagation direction and conjugate phase. This phase-conjugated photon will propagate in exactly the direction opposite to the incoming field. Such devices are used in phase-conjugate mirrors, which have the ability to cancel wavefront variations in a beam due to, for example, atmospheric turbulence. See ADAPTIVE OPTICS; OPTICAL PHASE CONJUGATION.

The suitability of available nonlinear optical materials is a critical factor in the development of nonlinear optical devices. For certain applications, silica glass fibers may be used. Because of the long propagation distances involved in intercontinental transmission systems, the small size of the optical nonlinearity in silica is not a drawback. Other key materials are semiconductors (such as gallium arsenide (GaAs), zinc selenide (ZnSe), and indium gallium arsenide phosphide (InGaAsP)), certain organic polymers such as liquid crystals, and semiconductor-doped glasses. See NONLINEAR OPTICS; OPTICAL MATERIALS. [D.R.A.]

## Nonlinear optics

A field of study concerned with the interaction of electromagnetic radiation and matter in which the matter responds in a nonlinear manner to the incident radiation fields. The nonlinear response is due to intensity-dependent variation of the propagation characteristics of the radiation fields or in the creation of radiation fields that propagate at new frequencies or in new directions. Nonlinear effects can take place in solids, liquids, gases, and plasmas, and may involve one or more electromagnetic fields as well as internal excitations of the matter.
