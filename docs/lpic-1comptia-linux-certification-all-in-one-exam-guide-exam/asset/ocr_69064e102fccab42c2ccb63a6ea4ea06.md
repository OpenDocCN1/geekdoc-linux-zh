placed current on the wire. If no current is present on the wire, then the CPU will continue working on whatever processing task has been assigned to it.

The interrupt system in a PC is very similar to a typical classroom. In a classroom setting, the instructor usually presents the material she has prepared to the students. If a student has a question, he can raise his hand and interrupt the instructor's presentation. After the question is answered, the instructor resumes the presentation.

PC interrupts work in much the same manner. Like the instructor, the CPU goes about its business until it is interrupted. Once interrupted, the CPU diverts its attention to the device that raised the interrupt. Once the device's request has been satisfied, the CPU goes back to what it was doing before.

The advantage to using interrupts is that the CPU services system devices only when they need it. It doesn't waste processing time on devices that are idle.

However, the scenario we've just discussed presents a problem. In a typical classroom, there are many students, not just one. Likewise, a PC system has many different devices that all need to get the CPU's attention from time to time. Unlike the hypothetical instructor we just discussed, the CPU has only a single INT wire. That would be sufficient if there were only a single device installed in the system. But this isn't the case. We need some way to allow many different devices to use that same INT wire. This is done using a *programmable interrupt controller* (PIC) chip.

The PIC chip has nine leads. One is connected to the INT wire on the CPU. The other eight are connected to interrupt wires in your motherboard's expansion slots. When a device in an expansion slot needs attention, it applies current to its interrupt wire. The PIC is alerted by this event and applies current to the CPU's INT wire. The CPU acknowledges the interrupt, and the PIC then tells the CPU which interrupt number was activated. The CPU can then service the device.

Early PCs had only eight interrupts and a single PIC, as just related. However, a modern PC has 16 interrupts. To get the extra interrupts, two PIC chips are actually cascaded together. That is, the wire that would normally be connected to the CPU INT wire on one PIC is connected instead to the second interrupt wire on the first PIC chip (whose INT wire is connected to the CPU). The second interrupt wire on the second PIC, which should be numbered INT 9, is actually wired to INT 2 in the expansion slots. Have you ever heard someone say that INT 2 and INT 9 are the same interrupt? Now you know why!

When working with interrupts, there are some important facts that you should keep in mind:

+   * Every device in the PC must be assigned an interrupt.
+   * Two ISA devices cannot share an interrupt.
+   * Two PCI devices can share interrupts.
+   * A PCI device cannot share an interrupt with an ISA device.
+   * Because INT 2 and INT 9 are actually the same wire on the PIC chips, you assign either one to a device in the system, but you can't assign both at the same time.