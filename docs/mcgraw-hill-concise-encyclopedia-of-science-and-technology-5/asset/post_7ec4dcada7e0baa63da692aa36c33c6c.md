
## Digital-to-analog converter
671

is to develop a single program which utilizes data supplied by the user to specify both the actions to be performed and the digital process elements and the schedule to be followed. Another approach is to develop a rather sophisticated operating system to supervise the execution of user programs, scheduling individual program elements for execution as specified by the user or needed by the process. **See** DIGITAL COMPUTER.

Many applications, particularly machining, manufacturing, and batch processing, involve large or complex operating schedules. Invariably, these can be broken down into simple logical sequences. Some applications—in the chemical process industries, in power generation, and in aerospace areas—require the use of traditional automatic control algorithms.

Attempts to expand the digital control medium through development of strictly digital control algorithms is an important and continuing trend. Such algorithms typically attempt to exploit the sampled nature of process inputs and outputs, significantly decreasing the sampling requirements of the algorithm. **See** CONTROL SYSTEMS. (D.A.M.)

## Digital counter

An instrument which, in its simplest form, provides an output that corresponds to the number of pulses applied to its input. Counters may be categorized into two types: the Moore machine or the Mealy machine. The simpler counter type, the Moore machine, has a single count input (also called the clock input or pulse input), while the Mealy machine has additional inputs that alter the count sequence. Digital counters take many forms, including geared mechanisms (tape counters and odometers are examples), relays (old pinball machines and old telephone switching systems), vacuum tubes (old test equipment), and solid-state semiconductor circuits (most modern electronic counters).

Most digital counters operate in the binary number system, since binary is easily implemented with electronic circuitry. Binary allows any integer (whole number) to be represented as a series of binary digits, or bits, where each bit is either a 0 or 1 (off or on, low, or high, or so forth).

Digital counters are found in much modern electronic equipment, especially equipment that is digitally controlled or has digital numeric displays. A frequency counter, as a test instrument or a channel frequency display on a radio tuner, consists simply of a string of decade counters that count the pulses of an input signal for a known period of time, and display that count on a seven-segment display. A digital voltmeter operates by using nearly the same idea, except that the counter counts a known frequency for a period of time proportional to the input voltage. **See** ANALOG-TO-DIGITAL CONVERTER.

A digital watch contains numerous counter/dividers in its large-scale integration (LSI) chip, usually implemented with complementary metal oxide semiconductor (CMOS) technology.

Digital computers may contain counters in the form of programmable interval timers that count an integral number of clock pulses of a known period, and then generate an output at the end of the count to signal that the time period has expired. Most of the counters in a microprocessor consist of arithmetic logic units that add one many-bit number to another, storing the results in a memory location. The program and data counters are examples of this kind of counter. **See** DIGITAL COMPUTER; MICROPROCESSOR.

Counters have progressed from relays to light-wavelength-geometry very-large-scale-integrated circuits. There are several technologies for building individual digital counters. Single-counters are available as integrated circuit chips in emitter-coupled logic, transistor-transistor logic, and CMOS. (M.E.W.)

## Digital filter

Any digital computing means that accepts as its input a set of one or more digital signals from which it generates as its output a second set of digital signals. While being strictly correct, this definition is too broad to be of any practical use, but it does demonstrate the possible extent of application of digital-filter concepts. **See** DIGITAL SIGNAL PROCESSOR, TERMINOLOGY.

**Capabilities.** Digital filters can be used in any signal-manipulating application where analog or continuous filters can be used. Because of their utterly predictable performance, they can be used in exacting applications where analog filters fail because of time- or other parameter-dependent coefficient drift in continuous systems. Because of the ease and precision of setting the filter coefficients, digital filters are an adaptable filter that are comparatively simple and particularly effective to implement. As digital technology becomes more ubiquitous, digital filters are increasingly acknowledged as the most versatile and cost-effective solutions to filtering problems.

The number of functions that can be performed by a digital filter far exceeds that which can be performed by an analog, or continuous, filter. By controlling the accuracy of the calculations within the filter (that is, the arithmetic word length), it is possible to produce filters whose performance comes arbitrarily close to the performance expected of the perfect models. For example, theoretical designs that require perfect cancellation can be implemented with great fidelity by digital filters.

**Linear difference equation.** The digital filter accepts as its input signals numerical values called *input samples* and produces its output signal numerical values called *output samples*. Each output sample at any particular sampling instant is a weighted sum of present and past input samples, and past output samples. If the sequence of input samples is $x_{n}$, $x_{n-1}$, $x_{n-2}$... then the corresponding sequence of output samples would be $y_{n}$, $y_{n-1}$, $y_{n-2}$... **SEE** DIFFERENCE EQUATION.

From this simple time-domain expression, a considerable number of definitions can be constructed. If the filter coefficients (the a's and the b's) are independent of the b's and v's, this digital filter is a linear filter. If the a's and b's are fixed, the digital filter is a linear time-invariant (LTI) filter. The order of the filter is given by the largest of the subscripts among the a's and b's, that is, the larger of M and N. If the b's are all zero (that is, if the output is the weighted sum of present and past input samples only), the digital filter is referred to as a nonrecursive (having no feedback) or finite impulse response (FIR) filter because the response of the filter to an impulse (actually a unit pulse) input is simply the sequence of the $a^*$ coefficients. If any value of b is nonzero, the filter is recursive (having feedback) and is generally an infinite impulse response (IIR) filter.

If the digital filter under consideration is not a linear, time-invariant filter, the transfer function cannot be used.

**Transfer functions.** Although the time-domain difference equation is a useful description of a filter, as in the continuous-domain filter case, a powerful alternative form is the transfer function. The information content of the transfer function is the same as that of the difference equation as long as a linear, time-invariant system is under consideration. A difference equation is converted to transfer-function form by use of the z transform. The z transform is simply the Laplace transform adapted for sampled systems with some shorthand notation introduced. **SEE** LAPLACE TRANSFORM; Z TRANSFORM.

**Adaptive filters.** So far only LTI filters have been discussed. An important class of variable-parameter filters change their coefficients to minimize an error criterion. These filters are called adaptive because they adapt their parameters in response to changes in the operating environment. An example is an FIR digital filter whose coefficients are continually adjusted so that the output will track a reference signal with minimum error. The performance criterion will be the minimization of some function of the error. **SEE** ELECTRIC FILTER. (S.A.W.)

## Digital-to-analog converter

A device for converting information in the form of combinations of discrete (usually binary) states or a signal to information in the form of the value or magnitude of some characteristics of a signal, in relation to a standard or reference. Most often, it is a device that has
