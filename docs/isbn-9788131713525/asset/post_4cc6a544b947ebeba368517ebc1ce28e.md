
## Appendix D

![](img/7a1144833e62564667e7dd9eb4c9f03d_522_0.png)

In this appendix

- SDRAM Basics page 492
- Clocking page 494
- SDRAM Setup page 495
- Summary page 500

At first glance, programming an SDRAM controller can seem like a formidable task. Indeed, numerous Synchronous Dynamic Random Access Memory (DRAM) technologies have been developed. In a never-ending quest for performance and density, many different architectures and modes of operation have been developed.

We examine the AMCC PowerPC 405GP processor for this discussion of SDRAM interface considerations. You might want to have a copy of the user manual to reference while we explore the issues related to SDRAM interfacing. This document is referenced in Section D.4.1, “Suggestions for Additional Reading.”

### D.1 SDRAM Basics

To understand SDRAM setup, it is necessary to understand the basics of how an SDRAM device operates. Without going into the details of the hardware design, an SDRAM device is organized as a matrix of cells, with a number of address bits dedicated to row addressing and a number dedicated to column addressing. Figure D-1 illustrates this.

![](img/7a1144833e62564667e7dd9eb4c9f03d_523_0.png)

**FIGURE D-1**
Simplified SDRAM block diagram

Inside the memory matrix, the circuitry is quite complex. A simplified example of a read operation is as follows: A given memory location is referenced by placing a row address on the row address lines and then placing a column address on the column address lines. After some time has passed, the data stored at the location addressed by the row and column inputs are made available to the processor on the data bus.

The processor outputs a row address on the SDRAM address bus and asserts its Row Address Select (RAS) signal. After a short preprogrammed delay to allow the SDRAM circuitry to capture the row address, the processor outputs a column address and asserts its Column Address Select (CAS) signal. The SDRAM controller translates the actual physical memory address into row and column addresses. Many SDRAM controllers can be configured with the row and column width sizes; the PPC405GP is one of those examples. Later you will see that this must be configured as part of the SDRAM controller setup.

This example is much simplified, but the concepts are the same. A burst read, for example, which reads four memory locations at once, outputs a single RAS and CAS cycle, and the internal SDRAM circuitry automatically increments the column address for the subsequent three locations of the burst read, eliminating the need for the processor to issue four separate CAS cycles. This is but one example of performance optimization. The best way to understand this is to absorb the details of an actual memory chip. An example of a well-written data sheet is included in Section D.4.1, “Suggestions for Additional Reading.”

#### D.1.1 SDRAM Refresh

An SDRAM is composed of a single transistor and a capacitor. The transistor supplies the charge, and the capacitor’s job is to retain (store) the value of the individual cell. For reasons beyond the scope of this discussion, the capacitor can hold the value for only a small duration. One of the fundamental concepts of dynamic memory is that the capacitors representing each cell must be periodically recharged to maintain their value. This is referred to as SDRAM refresh.

A refresh cycle is a special memory cycle that neither reads nor writes data to the memory. It simply performs the required refresh cycle. One of the primary responsibilities of an SDRAM controller is to guarantee that refresh cycles are issued in time to meet the chip’s requirements.

The chip manufacturers specify minimum refresh intervals, and it is the designer's job to guarantee it. Usually the SDRAM controller can be configured directly to select the refresh interval. The PowerPC 405GP presented here has a register specifically for this purpose. We will see this shortly.

### D.2 Clocking

The term *synchronous* implies that the data read and write cycles of an SDRAM device coincide with the clock signal from the CPU. SDR SDRAM is read and written on each SDRAM clock cycle. DDR SDRAM is read and written twice on each clock cycle, once on the rising edge of the clock and once on the falling edge.

Modern processors have complex clocking subsystems. Many have multiple clock rates that are used for different parts of the system. A typical processor uses a relatively low-frequency crystal-generated clock source for its primary clock signal. A phase locked loop internal to the processor generates the CPU's primary clock (the clock rate we speak of when comparing processor speeds). Because the CPU typically runs much faster than the memory subsystem, the processor generates a submultiple of the main CPU clock to feed to the SDRAM subsystem. You need to configure this clocking ratio for your particular CPU and SDRAM combination.

The processor and memory subsystem clocks must be correctly configured for your SDRAM to work properly. Your processor manual contains a section on clock setup and management, and you must consult this to properly set up your particular board design.

The AMCC 405GP is typical of processors of its feature set. It takes a single crystal-generated clock input source and generates several internal and external clocks required of its subsystems. It generates clocks for the CPU, PCI interface, Onboard Peripheral Bus (OPB), Processor Local Bus (PLB), Memory Clock (MemClk), and several internal clocks for peripherals such as timer and UART blocks. A typical configuration might look like those in Table D-1.

#### TABLE D-1
Typical PPC405GP Clock Configuration

| Clock | Rate | Comments |
| :--- | :--- | :--- |
| Crystal reference | 33MHz | Fundamental reference supplied to processor |
| CPU clock | 133MHz | Derived from processor's internal PLL, controlled by hardware pin strapping and register settings. |
| PLB clock | 66MHz | Derived from CPU clock and configured via hardware pin strapping and register settings. Used for internal processor local bus data interchange among its high-speed modules. |
| OPB clock | 66MHz | Derived from PLB clock and configured via register settings. Used for internal connection of peripherals that do not need high-speed connection. |
| PCI clock | 33MHz | Derived from PLB clock and configured via register settings. |
| MemClk | 100MHz | Drives the SDRAM chips directly. Derived from CPU clock and configured via register settings. |

Decisions about clock setup normally must be made at hardware design time. Pin strapping options determine initial clock configurations upon application of power to the processor. Some control over derived clocks is often available by setting divider bits accessible through processor internal registers dedicated to clock and subsystem control. In the example we present here based on the 405GP, final clock configuration is determined by pin strapping and firmware configuration. It is the bootloader's responsibility to set the initial dividers and any other clock options configurable via processor register bits very early after power is applied.

### D.3 SDRAM Setup

After the clocks have been configured, the next step is to configure the SDRAM controller. Controllers vary widely from processor to processor, but the end result is always the same: You must provide the correct clocking and timing values to enable and optimize the performance of the SDRAM subsystem.

As with other material in this book, there is no substitute for detailed knowledge of the hardware you are trying to configure. This is especially so for SDRAM. It is beyond the scope of this appendix to explore the design of SDRAM, but some basics must be understood. Many manufacturers' data sheets on SDRAM devices contain helpful technical descriptions. You are urged to familiarize yourself with the content of these data sheets. You don't need a degree in hardware engineering to understand what must be done to properly configure your SDRAM subsystem, but you need to invest in some level of understanding.

Here we examine how the SDRAM controller is configured on the 405GP processor as configured by the U-Boot bootloader we covered in Chapter 7, “Bootloaders.” Recall from Chapter 7 that U-Boot provides a hook for SDRAM initialization from the assembly language startup code found in start.S in the 4xx-specific cpu directory. Refer back to Section 7.4.4 “Board-Specific Initialization” in Chapter 7. Listing D-1 reproduces the sdram_init() function from U-Boot's.../cpu/ppc4xx/sdram.c file.

**Listing D-1**

```c
/**
 * ppc4xx sdram_init() from U-Boot
 */
void sdram_init(void)
{
    ulong sctrl;
    ulong rtr;
    int i;

    /*
     * Support for 100MHz and 133MHz SDRAM
     */
    if (get_bus_freq() > 100000000) {

        /* 133 MHz SDRAM */

        sctrl = 0x01074015;
        rtr = 0x07E00000;

    } else {

        /* default: 100 MHz SDRAM */

        sctrl = 0x0086400D;
        rtr = 0x05E00000;

    }

    for (i=0; i<NUM_BOCF; i++) {

        /* Disable memory controller. */

        mtdram0(mem_mccp01, 0x00000000);

        /* Set MBOCF for bank 0. */

        mtdram0(mem_nbOcf, mbOcf[i].reg);
```
