Circuit) bus. These three protocols share the same set of hardware pins, and so the software configuration tells the MSP430 how to clock them.
Software drivers use the bus protocols by instantiating a generic component, such as as Msp430Spi0C, Msp430Uart0C, and Msp430I2C0C. Each of these provides their functional interfaces and a Resource interface. Finally, they use a hardware-specific configuration interface. In the case of the SPI, for example, a client needs to configure the bus speed. This allows a client to place itself on the configurator path. Figure 11.2 shows this component structure.

# 11.2.7 Power lock library

TinyOS has a small library of reusable power lock components, which can be found in tos/system. They include:

+   - Two arbiters with different scheduling policies: FcfsArbiterC (first-come, first-served) and RoundRobinArbiterC (round-robin)

+   - Two power managers: ImmediatePowerManagerC and DeferredPowerManagerC

+   - Numerous configurators: as configurators are hardware-specific, they are spread throughout the code base, and are mostly in tos/chips.

If you want more detailed information on power locks, their performance, and use, please refer to TEPs 108 [13] and 115 [11], and to the paper describing them [12].

# 11.3 Exercises

+   1. The MSP430 ADC has a deferred power manager. Its timeout used to be 100 ms, but after some experiments it was changed to a timeout of 20 ms. Why 20 ms? Hint: look at how long it takes for the voltage reference to stabilize.

+   2. Why don’t radios typically have a power lock?

+   3. Compute the CPU cost of an atomic statement. Write a nested atomic section, where there is one atomic statement within another. Does the overhead go up?

+   4. Most interrupt handlers are themselves atomic: they are completely within an atomic statement. Try writing a UART byte reception interrupt handler that is re-entrant (can re-execute while already executing). Why is it hard? Can you do it without any atomic statements at all?