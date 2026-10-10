# 3.2 Integrated Processors: Systems on Chip

+   - Programmable timers
+   - JTAG interface for debugging

This is indeed a complete system on chip (SOC). Figure 3-2 is a block diagram of the AMCC PowerPC 440EP Embedded Processor. With the addition of memory chips and physical I/O hardware, a complete high-end embedded system can be built around this integrated microprocessor with minimal interface circuitry required.

![](bbox=[0.06, 0.28, 0.82, 0.63])

FIGURE 3-2
AMCC PPC 440EP Embedded Processor
(Courtesy AMCC Corporation)

Many manufacturers offer reference hardware platforms to enable a developer to explore the capabilities of the processor or other hardware. This examples later in this book (Chapters 14, “Kernel Debugging Techniques,” and 15, “Debugging Embedded Linux Applications”) were executed on the AMCC Yosemite board, which is the company’s reference platform containing the 440EP shown in Figure 3-2.

Numerous product configurations are available with PowerPC processors. As demonstrated in Figure 3-2, the AMCC 440EP contains sufficient I/O interfaces