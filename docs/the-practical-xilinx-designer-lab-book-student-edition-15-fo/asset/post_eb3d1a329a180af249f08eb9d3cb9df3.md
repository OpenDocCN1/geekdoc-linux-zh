
![](img/5124daf79d2807d81e49f49c22f1f8c1_386_0.png)

## Figure 10.10 DWARF's I/O port circuitry.

enter a metastable state due to a change on one of the inputs just as a clock edge occurs.

Figure 10.11 shows the circuitry for detecting and recording the state of interrupts. A rising edge on the interrupt input (INT) loads a logic one into the first D flip-flop. The logic one propagates through the INTRPT_DFF0 flip-flop and appears on the INTRPT output on the next rising edge of CLOCK. This synchronizes the interrupt to DWARF's clock and reduces the chances of entering a metastable state.

In addition to a flip-flop to record the occurrence of an interrupt, DWARF also needs a flip-flop to indicate when it is executing an interrupt service routine. The IFLAG0 flip-flop serves this purpose. IFLAG0 is set to a logic one state when SET_IFLAG=1. The IFLAG output from the flip-flop is used to switch to the alternate set of eight registers in the DWARF_REG module. Also, both IFLAG and INTRPT are inputs to the instruction decoder. If INTRPT=1 and IFLAG=0, the instruction decoder will alter the flow of instructions by initiating the interrupt service routine. But if INTRPT=1 and IFLAG=1, DWARF will ignore the pending interrupt because it is already processing an interrupt.

![](img/5124daf79d2807d81e49f49c22f1f8c1_387_0.png)

## Figure 10.11 DWARF's interrupt-handling circuitry.

The interrupt flip-flops are cleared when the CLR_INTRPT and CLR_IFLAG are high. The CLR_INTRPT signal is asserted to clear the INTRPT flag when the interrupt routine is entered. This minimizes the amount of time that passes before the circuitry can detect another interrupt. The CLR_IFLAG signal, however, is asserted as the processor is leaving the ISR. The RESET signal also clears the INTRPT and IFLAG flip-flops so that DWARF does not erroneously begin processing an interrupt when it first starts up.

Figure 10.11 also shows how the clock and reset signals enter DWARF. Both the IN_RESET and IN_CLOCK inputs enter through normal IBUFs. But the IN_CLOCK input then passes through a primary global buffer (symbol BUFG P). The use of such a buffer allows the clock signal to travel over a global net that does not suffer from the delays incurred by signals that travel through the routing switches. Thus, the CLOCK signal has very low skew and clock edges will reach all the flip-flops at nearly the same instant.

The bidirectional data bus interface to the external RAM is shown in Figure 10.12. Data values on the D bus are driven out of DWARF onto the

[DATA7..DATA0] pins when WRITE=1. This enables the tristate output buffers (OBUFES). When the tristate gates are disabled, it is possible for an external device (the RAM in this case) to drive a value onto the DATA bus. The value can reach the internal circuitry of DWARF by placing a logic one on the DRV_D_DATA signal. That enables the internal tristate buffers (BUFES) so the value on the DATA bus will appear on the internal D bus.

![](img/5124daf79d2807d81e49f49c22f1f8c1_388_0.png)

## Figure 10.12 DWARF's instruction register and data bus interface.

The instruction register (module IR0) is connected directly to the DATA bus before it reaches the internal tristate buffers. Therefore, the instruction register is loaded with whatever value is on the [DATA7..DATA0] pins (this will be an opcode fetched from the RAM). The loading occurs on the rising edge of CLOCK when LD_IR=1. The instruction register is cleared when RESET is asserted.

The final module is the DWARF instruction decoder (Figure 10.13). It receives the carry and zero flags, interrupt status signals, and the 8 bits of the instruction register as inputs. The instruction decoder outputs 29 signals that control the circuitry we have already discussed.

The instruction decoder module was created by importing a netlist synthesized from the ABEL code in Listing 10.1 or the VHDL code in Listing 10.2. The listing is quite long because DWARF has twice as many instructions as GNOME. We will go over a few of the instruction sequences (with line numbers for the VHDL version of the code indicated in bold). The remainder of the code should be decipherable after that.
