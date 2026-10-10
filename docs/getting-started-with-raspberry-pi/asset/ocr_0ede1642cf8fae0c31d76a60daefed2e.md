The UART usually found on PCs is National Semiconductor's 16550, or compatible chips from other vendors, so you will find references to "16550-type UART" in code and documentation. The 8250 chip is the predecessor of the 16550, so the Linux driver for PC UARTs is named **8250.c**.

# Layered Architecture

As you just saw, the users of the serial subsystem are many and different. This has motivated kernel developers to structure a layered serial architecture using the following building blocks:

+   1. Low-level drivers that worry about the internals of the UART or other underlying serial hardware.
+   2. A tty driver layer that interfaces with the low-level driver. A tty driver insulates higher layers from the intricacies of the hardware.
+   3. Line disciplines that "cook" data exchanged with the tty driver. Line disciplines shape the behavior of the serial layer and help reuse lower layers to support different technologies.

To help custom driver implementations, the serial subsystem also provides core APIs that factor commonalities out of these layers.

**Figure 6.2** shows the connection between the layers. N_TTY, N_IRDA, and N_PPP are drop-in line disciplines that mold the serial subsystem to respectively support terminals, Infrared, and dialup networking. **Figure 6.3** maps the serial subsystem to kernel source files.

# Figure 6.2. Connection between the layers in the serial subsystem.