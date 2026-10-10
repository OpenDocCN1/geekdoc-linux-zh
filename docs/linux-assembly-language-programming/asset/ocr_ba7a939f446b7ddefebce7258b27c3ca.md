# **Nested interrupts**

Most computers prioritize interrupts and then allow higher priority interrupts to interrupt those of lower priority. This kind of policy is called a *nested interrupt* policy. Implementing a nested interrupt policy on an x86 requires that both the interrupt controller and the programmer be given more responsibility. On the x86 the programmer has control over the interrupt enable flag. The

STI
command sets the interrupt enable flag. The

CLI

command clears it. By including an $STI$ command at the beginning of an ISR, the programmer can override the default one-at-a-time policy and make an ISR interruptible. Interrupts cannot be nested if they execute with the interrupt enable flag cleared.

There is also more work for the interrupt controller. If the x86 executes ISRs with the interrupt enable flag set, then the interrupt controller has to assume responsibility for enforcing the priority system. Since the processor has its guard down, the interrupt controller must not let every incoming interrupt pass through. Otherwise, as noted above, the ISRs could play ping-pong with the processor. In particular, the controller is responsible for not interrupting an interrupt unless the ISR being interrupted has a lower priority than the one it is allowing through. If the ISR executing has equal or higher priority, then the pending interrupt must wait until the ISR is finished. But in order for the controller to hold off the pending interrupt until then, it needs to know when the ISR gets done. It needs a signal. Without a signal it has no way of knowing. If it doesn't know whether a high priority ISR is finished executing, then it cannot decide whether it is okay to interrupt the CPU with a low priority interrupt or not. Since the interrupt controller has its own read cycle, one might expect a write cycle for this purpose.

# **The EOI Command**

Since the x86 does not have an I/O controller write cycle, it falls to the lot of the programmer to include an "All Done" message to the interrupt controller at the end of each ISR. This message is called an EOI, or *end of interrupt* command.

So that the interrupt controller can receive communications from the processor, it has an I/O address. The programmer can then use an $OUT$ command to issue the EOI. The I/O address is also used when the interrupt controller gets programmed. As noted above, it needs to be programmed so that it knows what interrupt numbers to report.

As a device with an I/O address, the interrupt controller looks like just any other I/O device. But it is special in that it is the only I/O device that can signal the processor directly. All the others must go through the interrupt controller.

# **9.2.3 The NMI and RESET Interrupts**

Besides the general-purpose interrupt pin on the x86, there are two other interrupt pins. They are the NMI and RESET pins.

A signal on the NMI, or *nonmaskable interrupt* pin, is not blocked by clearing the interrupt enable flag. It does not trigger an interrupt acknowledge bus cycle. It is serviced by interrupt service routine number 2. It is used to signal parity errors in memory or power supply problems.

The RESET pin is intended for use in situations where there may be no interrupt descriptor table in memory. For example, when the computer is being turned on. Consequently, there is no point in storing an address for it in the interrupt table. Instead the address is built into the processor. That address is FFFF0H (or FFF0H on the 8086). It is easily remembered as $-16$ in two's complement. The read-only memory at this