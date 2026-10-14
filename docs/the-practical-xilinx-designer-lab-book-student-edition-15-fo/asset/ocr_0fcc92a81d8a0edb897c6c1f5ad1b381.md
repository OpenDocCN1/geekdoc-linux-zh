![](bbox=[0.24, 0.08, 0.92, 0.58])

# Figure 10.3 DWARF's register set and ALU

When executing instructions, DWARF often needs a "scratch-pad" register where it can store intermediate values and addresses. R0 is selected for this purpose. But the instruction decoder needs a means of addressing this register when it needs to. For this reason, a logic one applied to the ROA or ROB input forces the address of R0 onto the A_ADDR or B_ADDR input, respectively, regardless of the register address stored in the instruction register.

The register set actually contains 16 registers, so the BANK_SEL input selects one of two banks of eight registers. The IFLAG signal is high during the execution of an interrupt service routine, and this is used to switch the register banks. This gives the interrupt service routine its own set of registers to use and prevents it from altering the values in the registers used during DWARF's normal operations.

The value on the B_OUT output of the register set can be driven onto the D bus by raising the DRV_D_REG signal. This enables the drivers of the internal tristate buffer (BUFES) so the register value can pass through. This operation is needed when a value from the register set is being transferred to another section of DWARF's circuitry or into external RAM.

The details of the DWARF register set are shown in Figure 10.4. The heart of the register set is a dual-port synchronous RAM (RAM16X8D) from the standard