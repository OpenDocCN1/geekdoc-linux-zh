The next instruction, load R0, has 0100 as the most-significant 4 bits of the encoding. The remaining 4 bits encode the address of the data RAM location. In this case that is RAM location zero, so the least-significant 4 bits are 0000 and the total opcode is 01000000.

As a final example, the instruction jump halt performs a program jump to the address labeled halt. The actual address associated with the label halt is seven (0000111 in 7-bit binary). The first bit of a jump instruction opcode is 1. The final 7 bits of the opcode is the address to jump to. So the opcode for the jump halt instruction is 10000111. That's all there is to it.

Once the opcodes are stored in the program memory, the GNOME can read out the bit patterns and execute the program. But what are the individual steps that must occur to execute each instruction? Each instruction has three basic steps:

Fetch: The GNOME must read the current instruction from the program memory and store it into the instruction register.

Decode: The GNOME must figure out which type of instruction is to be executed and get the required operands.

Execute: The GNOME must do the operation on the operands and store the result.

Table 9.3 shows these steps for each of the GNOME instructions. During the fetch step, a new instruction opcode is read from the address in the external RAM that is pointed to by the PC. This opcode is stored in the instruction register (IR). The program counter is also incremented so that it points to the next instruction (since all the GNOME instructions are 1 byte long).

During the decode step, the instructions will require different operations depending upon their addressing mode. For example, an instruction that uses direct addressing, like add Rd, first needs to get its data from memory. This is done by accessing the external memory with the memory address stored in the lower four bits of the opcode. The four-bit value read from memory replaces these address bits in the instruction register. On the other hand, immediate mode instructions like the load immediate data instruction (load #d) don't do anything during the decoding step because they already have their operands.

In the final execute step, the instruction is completed. To continue the description of the direct add instruction, the accumulator is loaded with the sum of the operand data (stored in the lower 4 bits of the IR), the current value in the accumulator, and the carry flag. As another example, the store Rd instruction stores the value in the accumulator into the memory location whose address is stored in the lower 4 bits of the opcode. Finally, the skip_c and skip_z instructions will increment the PC again (which will jump over the next instruction after the skip instruction) if the C or Z flag is set, respectively.