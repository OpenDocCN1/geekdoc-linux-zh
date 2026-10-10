# Infrared

Infrared (IR) rays are optical waves lying between the visible and the microwave regions of the electromagnetic spectrum. One use of IR is in point-to-point data communication. Using IR, you can exchange visiting cards between PDAs, network two laptops, or dispatch a document to a printer. IR has a range of up to 1 meter within a 30-degree cone, spreading from −15 to +15 degrees.

There are two popular flavors of IR communication: Standard IR (SIR), which supports speeds of up to 115.20 Kbaud; and Fast IR (FIR), which has a bandwidth of 4Mbps.

Figure 16.4 shows IR connection on a laptop. UART1 in the Super I/O chipset is IR-enabled, so an IR transceiver is directly connected to it. Laptops having no IR support in their Super I/O chip may rely on an external IR dongle (see the section "Device Example: IR Dongle") similar to the one connected to UART0. Figure 16.5 shows IR connection on an embedded SoC having a built-in IR dongle connected to a system UART.

# Figure 16.4. IrDA on a laptop.

![](bbox=[0.29, 0.36, 0.7, 0.66])

# Figure 16.5. IrDA on an embedded device (for example, EP7211).