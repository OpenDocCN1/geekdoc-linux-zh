will not work without them), the RC circuit sets frequency, there is a resistive positive feedback path (to make the mathematical possibility $u_0 (= 0)$ unstable, and the saturation behavior of the amplifier sets the amplitude of oscillation at the output to $\pm V_{sat}$.

Relaxation oscillators that have a low duty cycle—that is, produce output pulses whose durations are a small fraction of the overall period— are sometimes called blocking oscillators because their operation is characterized by an "on" transient that "blocks" itself, followed by a recovery period.

Inverters (digital circuits that invert a logic signal, so that a 0 at the input produces a 1 at the output, and vice versa) are essentially voltage amplifiers and can be used to make relaxation oscillators in a number of ways. A circuit related to that of the illustration uses a loop of two inverters and a capacitor $C$ to provide positive feedback, with a resistor $R$ in parallel with one of the inverters to provide an $RC$ charging time to set frequency. This circuit is commonly given as a simple example, but there are a number of problems with using it, such as that the input voltage to the first gate sometimes exceeds the specified limits for practical gates. A more practical digital relaxation oscillator, called a ring oscillator, consists simply of a ring containing an odd number $N$ (greater than 1) of inverters. See LOGIC CIRCUITS.

Sine-wave oscillators. Oscillators in the second major class have their oscillation frequency set by a linear circuit, and their amplitudes set by a weak nonlinearity.

A simple example of a suitable linear circuit is a two-component loop consisting of an ideal inductor (whose voltage is given by Eq. (3), where $i$ is its current) and a capacitor (whose

```
$v = L\frac{di}{dt}$  (3)
```

current is given by Eq. (4)), connected in parallel. These are said to be linear elements because, in a sense, the output is directly proportional to input: for example, doubling the voltage $v$ across a capacitor also doubles $dv/dt$ and therefore doubles $i$. The overall differential equation for a capacitor-inductor loop can be written as Eq. (5).

```
$i = C\frac{dv}{dt}$  (4)
```

```
$i + LC\frac{d^2i}{dt^2} = 0$  (5)
```

Mathematically this has solutions of the form of Eq. (6), where

```
$i = A\sin(\omega t + \phi)$  (6)
```

$\omega = 1/\sqrt{LC}$ [which means that the circuit oscillates at a frequency $1/(2\pi\sqrt{LC})$] and $A$ and $\phi$ are undefined. They are undefined precisely because the elements in the circuit are linear and do not vary with time; any solution (possible behavior) to the equation can be scaled arbitrarily or time-shifted arbitrarily to give another. Practically, $A$ and $\phi$ are determined by weak nonlinearities in a circuit. See DIFFERENTIAL EQUATION; LINEARITY.

Equation (5) is a good first approximation to the equation describing a pendulum, and so has a long history as an accurate timekeeper. Its value as an oscillator comes from Galileo’s original observation that the frequency of oscillation ($\omega/2\pi$) is independent of the amplitude $A$. This contrasts sharply with the case of the relaxation oscillator, where any drift in the amplitude (resulting from a threshold shift in a comparator, for instance) can translate directly into a change of frequency. Equation (5) also fundamentally describes the operation of the quartz crystal (that has replaced the pendulum as a timekeeper; the physical resonance of the crystal occurs at a time constant defined by its spring constant and its mass. See HARMONIC MOTION; HARMONIC OSCILLATOR; PENDULUM.

Frequency locking. If an external signal is injected into an oscillator, the natural frequency of oscillation may be affected. If the external signal is periodic, oscillation may lock to the external

# Oscillatory reaction 1583

frequency, a multiple of it, or a submultiple of it, or exhibit an irregular behavior known as chaos. See CHAOS.

This locking behavior occurs in all oscillators, sometimes contrary to intended behavior (as when an oscillator locks unintentionally to a harmonic of the power-line frequency) and sometimes by design. An important example of an oscillator that exploits this locking principle is the human heart. Small portions of heart muscle act as relaxation oscillators. They contract, periodically producing an output voltage that is coupled to its neighbors. For a short time the muscle then recovers from the contraction. As it recovers, it begins to become sensitive to externally applied voltages that can trigger it to contract again (although it will eventually contract anyway). Each small section of heart muscle is thus an independent oscillator, electrically coupled to its neighbors, and the whole heart is synchronized by the frequency-locking mechanism. See CARDIAC ELECTROPHYSIOLOGY.

# Oscillatory reaction

A chemical reaction in which some composition variable of a chemical system exhibits regular periodic variations in time or space. It is a basic tenet of chemistry that a closed system moves inexorably toward an unchanging static state called chemical equilibrium. That motion can be described by the monotonic increase of entropy if the system is isolated, and by the monotonic decrease of Gibbs free energy if the system is constrained to constant temperature and pressure. See CHEMICAL EQUILIBRIUM; ENTROPY.

The species taking part in a chemical reaction can be classified as reactants, products, or intermediates. The concentrations of reactants decrease. Intermediates are formed, then steps and destroyed by others. If there is only one intermediate $C_1$ and if its concentration is always much less than the initial concentrations of reactants, this intermediate attains a stable steady state in which the rates of formation and destruction are virtually equal. Some oscillations require at least two intermediates which interact in such a way that the steady state of the total system is unstable to the minor fluctuations present in any collection of molecules. The concentrations of the intermediates may then oscillate regularly, although the oscillations must disappear before the inevitable monotonic approach to equilibrium.

The systems whose chemistries are best understood all involve an element that can exist in several different oxidation states. An example is the so-called Belousov-Zhabotinsky reaction. A strong oxidizing agent (bromate) attacks an organic substrate (such as malonic acid), and the reaction is catalyzed by a metal ion (such as cerium) that can exist in two different oxidation states.

As long as bromide ion (Br$^-$) is present, it is oxidized by bromate (BrO$_3^-$), as in reaction (1).

```
$BrO_3^- + 2Br^- + 3H^+ \rightarrow 3HOBr$  (1)
```

When bromide ion is almost entirely consumed, the iron ion (Ce$^{3+}$) is oxidized, as in reaction (2). Reaction (2) is inhibited by Br$^-$, but when the concentration of HOBr can no longer be reduced to a critical level, reaction (2) accelerates autocatalytically until bromate is being reduced by Ce$^{3+}$ many times as rapidly as it is by Br$^-$ when reaction (3) is dominant.

```
$BrO_3^- + 4Ce^{3+} + 5H^+ \rightarrow HOBr + 4Ce^{4+} + 2H_2O$  (2)
```

The hypobromous acid (HOBr) brominates the organic substrate to form bromomalic acid (BrMA), as in reaction (3).