In order to allow programmers to avoid relying on polling, processors have at least one input pin which allows I/O devices to signal the processor when they need the processor to do something. Such a pin is called an *interrupt pin*. An interrupt pin makes it possible for an I/O device to initiate communication with the CPU. A CPU without an interrupt pin has been compared to a telephone without a bell.

Suppose that a printer is connected to an interrupt pin on the CPU, as shown in Figure 9-1. With the printer hooked up to the CPU in this way, the CPU would be able to ignore the printer until it received a signal. It could then process a printer character and return to its main job. There would be relatively little wasted time. This setup would work fine if the printer were the only I/O device which ever needed attention. But of course there are many such devices.

# Figure 9-1. A Computer with Only One Interrupt

![](bbox=[0.18, 0.24, 0.82, 0.41])

To allow for several I/O devices, one might expect there to be several interrupt pins on the processor. The x86 architecture does not do things this way. It has only one general-purpose interrupt pin. It delegates the arbitration of interrupt signals to an external circuit called the *interrupt controller circuit*, as shown in Figure 9-2. This figure also shows an IRQ bus from the I/O system to the interrupt controller circuit. An IRQ bus consists of wires from various I/O devices. Each device that needs interrupt service is given one of the wires on this bus, assuming that there are enough of them to go around, that is. The IRQ bus wires are numbered IRQ0, IRQ1, etc. IRQ stands for *interrupt request* line. The numbers 0, 1, etc., encountered in this context are called *IRQ numbers*.

# Figure 9-2. A Computer with an Interrupt Controller

![](bbox=[0.18, 0.62, 0.82, 0.77])

The interrupt controller allows several I/O devices to have a signal path to the CPU even though the x86 has only one general-purpose interrupt pin.

# 9.2.1 x86 Interrupt Handling

When an x86 processor receives an interrupt signal, it first completes the instruction it is currently working on. Then, provided a special flag has not been cleared, it handles the interrupt in three steps.

**Step 1.**

It reads the number of the interrupt responsible for the interrupt signal from the interrupt controller.