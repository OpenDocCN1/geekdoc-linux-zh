# 1496 Nonlinear optical devices

balanced on top of a gimbaled thruster engine (illus. b), and a controlled robot arm (illus. c). Newton's second law of motion for the pendulum is Eq. (1), where m(t) is the mass of the bob,

$$m\ddot{u}(t)=\frac{m g}{L}\sin(u(t)-ut)$$

$$(1)$$

$\ell$ is the length of the pendulum, and g is the acceleration due to gravity. By choosing the angular position $\theta=x_1$ and angular velocity $\dot{\theta}=x_2$ of the bob as the state of the system, Eq. (1) can be rewritten as two first-order state equations (2).

$$\begin{array}{l} \dot{x}_1=x_2 \\ \dot{x}_2=\frac{g}{\ell}\sin x_1+u \end{array}$$

$$(2)$$

See PENDULUM.

If the torque is absent ($u=0$), the upright position of a motionless pendulum ($x_1=0$, $\dot{x}_2=0$) is an equilibrium state: $x_1=0$, $\dot{x}_2=0$. If the pendulum is slightly perturbed at this state, it will fall down and keep oscillating around the other equilibrium point at $x_1=\pi$ and $\dot{x}_2=0$, where again, $x_1=0$ and $\dot{x}_2=0$. To keep the pendulum in the upright position in physically realistic situations involving perturbations, the torque u is chosen to be a suitable function $\phi$ of the state $x_1$, $x_2$, as in Eq. (3). That

$$u=\phi(x_1,x_2)$$

$$(3)$$

u should be a feedback control law in terms of the state is one of the most important results of control theory. [D.D.S.]

# Nonlinear optical devices

Devices that use the fact that the polarization (or any real medium) is a nonlinear function of the optical field strength to implement various useful functions. The nonlinearities themselves can be grouped roughly into second-order and third-order. Materials that possess inversion symmetry typically exhibit only third-order nonlinearities, whereas materials with inversion symmetry can exhibit both second- and third-order nonlinearities. See CRYSTALLOGRAPHY; ELECTRIC SUSCEPTIBILITY; ELECTROMAGNETIC RADIATION; POLARIZATION OF DIELECTRICS.

# Second-order devices

Devices based on the second-order nonlinearity involve three-photon (or three-wave) mixing. In this process, two photons are mixed together to create a third photon, subject to energy- and momentum-conservation constraints. Different photons are ascribed to this mixing process, depending upon the relative magnitudes of the energies of the participating photons. See CONSERVATION OF ENERGY; CONSERVATION OF MOMENTUM. When the two beginning photons are of equal energy or frequency, the mixing process gives a single photon with twice the energy or frequency of the original one. This mixing process is called second-harmonic generation. Second-harmonic generation is used only in devices where photons of visible frequency are desired but the available underlying laser system is capable of producing only infrared photons. For example, the neodymium-doped yttrium-aluminum-garnet (Nd:YAG) laser produces photons in the infrared with a wavelength of 1.06 micrometers. These photons are mixed in a crystal with a large second-order nonlinearity and proper momentum-conservation characteristics to yield green second-harmonic photons of 0.532-$\mu$m wavelength. Under different momentum-conservation constraints, a similar interaction can take place between two photons of different frequency, resulting in photons whose energy or frequency is the sum of those of the original photons. This process is called sum-frequency mixing. See LASER.

Optical parametric oscillation/amplification occurs when one of the two initial photons has the largest energy and frequency of the three. A high-energy photon and a low-energy photon mix to give a third photon with an energy equal to the difference between the two initial photons. If initially the third field amplitude is zero, it is possible to generate a third field from nothing; in this case the process is called optical parametric oscillation. If the third field exists but at a low level, it can be amplified through the optical parametric amplification process. See PARAMETRIC AMPLIFIER.

# Third-order devices

Devices based on the third-order nonlinearity involve a process called four-photon (or four-wave) mixing. In this process, three photons are mixed together to create a fourth photon, subject to energy- and momentum-conservation constraints. The four-photon mixing nonlinearity is responsible for the existence of so-called self-action effects where the refractive index and absorption coefficient of the optical field are modified by the light field's own presence. For third-harmonic generation and related processes, and for phase-conjugation processes.

In a medium with a third-order nonlinearity, the refractive index and absorption coefficient of a light field present in the medium are modified by the strength of the light intensity. Because the field effectively acts on itself, this interaction is termed a self-action effect. The momentum-conservation constraints are automatically satisfied because of the degenerate frequencies involved in the interaction. Such an interaction manifests itself by changing the total absorption experienced by the light field as well as by changing the velocity of propagation of the light field. See ABSORPTION OF ELECTROMAGNETIC RADIATION; REFRACTION OF WAVES.

There are many devices based on the self-action effects. A reverse saturable absorber becomes more opaque because of the nonlinear absorption (also called two-photon absorption) that it manifests. Refractive-index changes can be used to change the transmission characteristics of resonant cavities and other structures by modifying the effective optical path length (the product of actual structure length times the effective refractive index for the structure) and shifting the cavity resonances to other frequencies. Several nonlinear optical switches have been proposed based upon this resonance-shifting phenomenon. See CAVITY RESONATOR; OPTICAL STABILITY.

In a third-harmonic generation process, three photons of like energy and frequency are mixed to yield a single photon with three times the energy and frequency of the initial photons. Applications of third-harmonic generation are typical in the areas of frequency conversion.

Phase-conjugation devices make use of a property that third-order media possess whereby energy- and frequency-degenerate photons from two counterpropagating fields are mixed with an incoming photon to yield a photon with exactly the opposite propagation direction and conjugate phase. This phase-conjugated photon will pass through the cavity resonator in exactly the direction opposite to the incoming field. Such devices are used in phase-conjugate mirrors, mirrors which have the ability to cancel wave variation in a beam due to, for example, atmospheric turbulence. See ADAPTIVE OPTICS; OPTICAL PHASE CONJUGATION.

The suitability of available nonlinear optical materials is a critical factor in the development of nonlinear optical devices. For certain applications, silica glass fibers may be used. Because of the long propagation distances involved in intercontinental transmission systems, the small size of the optical nonlinearity in silica is not a drawback. Other key materials are semiconductors (such as gallium arsenide (GaAs), zinc selenide (ZnSe), and indium gallium arsenide phosphide (InGaAsP)), certain organic polymers such as liquid crystals, and semiconductor-doped glasses. See NONLINEAR OPTICS; OPTICAL MATERIALS. [D.R.A.]

# Nonlinear optics

A field of study concerned with the interaction of electromagnetic radiation and matter in which the matter responds in a nonlinear manner to the incident radiation fields. The nonlinear response is due to intensity-dependent variation of the propagation characteristics of the radiation fields or in the creation of radiation fields that propagate at new frequencies or in new directions. Nonlinear effects can take place in solids, liquids, gases, and plasmas, and may involve one or more electromagnetic fields as well as internal excitations of the