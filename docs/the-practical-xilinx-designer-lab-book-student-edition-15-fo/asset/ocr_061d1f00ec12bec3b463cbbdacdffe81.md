# Interrupt Handling

Subroutine calls and returns occur under the direction of the program. There are situations, however, when external conditions demand immediate attention and the flow of control must be abruptly changed. These interrupts are not events that the microprocessor can anticipate and plan for. Instead, it must save enough information about its current state, jump to a section of code that handles the interrupt (called an interrupt service routine or ISR), and then restore its state and continue its original flow of instructions.

The state information that the microprocessor must store after an interrupt is received is, at minimum, the value of the program counter. With this information, the microprocessor can return to where it was after it finishes processing the interrupt. But the microprocessor must also save the values in registers and flags as well if these might be altered by the instructions that service the interrupt. The values of the PC, registers, and flags at any given time are typically called the context. A common technique for saving the context is to push the values onto the stack using the same techniques employed during subroutine calls. Then the context can be restored by popping it off the stack at the end of the ISR.

# Experimental

We have touched on the basic ideas, so now it is time to implement them in the DWARF microprocessor. This design is oriented toward the XC4005XL FPGA because it has more left-over resources than the XC95108 CPLD, so it will be an easier fit. The XC4005XL also has internal tristate buffers and built-in RAMs that we will use in the DWARF design. This is not to say that the DWARF architecture cannot be implemented in an XC9500 CPLD, but we will not do it here.

Table 10.1 shows the DWARF instruction set. There are twice as many instructions as found in the GNOME. Here are the main differences from the GNOME instruction set:

+   1. The load and store instructions have been extended with register, indexed, and indirect addressing modes.
+   2. An in instruction was added that loads the value on an input port into one of the eight internal registers. The out instruction sends the value in the accumulator to an output port.
+   3. The xor, add, and test instructions have been restricted to using the internal registers as operands.
+   4. The skip_c and skip_z instructions were replaced with the jc and jz instructions, which can jump to any location in the PROGRAM region if the carry or zero flag is set, respectively.