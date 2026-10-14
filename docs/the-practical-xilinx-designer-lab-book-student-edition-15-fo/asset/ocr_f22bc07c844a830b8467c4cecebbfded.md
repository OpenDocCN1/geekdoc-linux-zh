DWARF's memory address generation circuitry is shown in Figure 10.8. The program counter (top left) shows that the PC (with reference identifier of PC0) is just an 8-bit, loadable counter from the standard part list (CB8CLE).

A logic one on the LD_PC input will load the PC with a new value from the D bus on the next rising edge of CLOCK. This operation is used for jumps within the program. On the other hand, a logic one on the INC_PC input will cause the PC to increment its value. This operation is needed during the normal sequential execution of instructions.

The value in the program counter can be driven onto the D bus by raising the DRV_D_PC signal. This enables the drivers of the internal tristate buffer (BUFES) so the PC value can pass through. This operation is needed when the value in the PC is being stored on the stack in external RAM.

The PC is cleared by raising the RESET or CLR_PC signals. This operation is needed when DWARF first starts so that program execution can begin at address 0 in the PROGRAM region. The program counter is also cleared at the beginning of an ISR.

Looking next at the stack pointer (Figure 10.8, bottom left) shows that the SP (with reference identifier of SP0) is just an 8-bit, loadable, up/down counter from the standard part list in the schematic editor (CC8CLED).

![](bbox=[0.28, 0.73, 0.92, 0.92])

# Figure 10.8 DWARF's program counter, stack pointer, address selector, and RAM control circuitry.