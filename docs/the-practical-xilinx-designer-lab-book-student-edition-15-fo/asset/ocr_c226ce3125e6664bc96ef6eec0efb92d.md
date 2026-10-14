![](bbox=[0.18, 0.08, 0.88, 0.62])

# Figure 10.10 DWARF's I/O port circuitry.

enter a metastable state due to a change on one of the inputs just as a clock edge occurs.

Figure 10.11 shows the circuitry for detecting and recording the state of interrupts. A rising edge on the interrupt input (INT) loads a logic one into the first D flip-flop. The logic one propagates through the INTRPT_DFF0 flip-flop and appears on the INTRPT output on the next rising edge of CLOCK. This synchronizes the interrupt to DWARF's clock and reduces the chances of entering a metastable state.

In addition to a flip-flop to record the occurance of an interrupt, DWARF also needs a flip-flop to indicate when it is executing an interrupt service routine. The IFLAG0 flip-flop serves this purpose. IFLAG0 is set to a logic one state when SET_IFLAG=1. The IFLAG output from the flip-flop is used to switch to the alternate set of eight registers in the DWRF_REG module. Also, both IFLAG and INTRPT are inputs to the instruction decoder. If INTRPT=1 and IFLAG=0, the instruction decoder will alter the flow of instructions by initiating the interrupt service routine. But if INTRPT=1 and IFLAG=1, DWARF will ignore the pending interrupt because it is already processing an interrupt.