
## Table 9.2 GNOME instruction set opcodes.

| Mnemonic | Encoding | Comments |
|---|---|---|
| load Rd | 0100 d3 d2 d1 d0 | d3..d0 are the address bits of a RAM location in the range [0..15]. |
| load #d | 0001 d3 d2 d1 d0 | d3..d0 are the bits of a value in the range [0..15]. |
| store Rd | 0011 d3 d2 d1 d0 | d3..d0 are the address bits of a RAM location in the range [0..15]. |
| add Rd | 0101 d3 d2 d1 d0 | d3..d0 are the address bits of a RAM location in the range [0..15]. |
| add #d | 0010 d3 d2 d1 d0 | d3..d0 are the bits of a value in the range [0..15]. |
| xor Rd | 0110 d3 d2 d1 d0 | d3..d0 are the address bits of a RAM location in the range [0..15]. |
| test Rd | 0111 d3 d2 d1 d0 | d3..d0 are the address bits of a RAM location in the range [0..15]. |
| clear_c | 00000000 |  |
| set_c | 00000001 |  |
| skip_c | 00000110 |  |
| skip_z | 00000111 |  |
| jump #a | 1 a6 a5 a4 a3 a2 a1 a0 | a7..a0 are the bits of an address in the range [0..127]. |

and fill in any immediate data or address bits that are required. Figure 9.5 shows the machine code associated with the instructions for the 8-bit addition program. The first instruction is clear_c, which has an encoding of 00000000. This 8-bit opcode is placed in the program at address zero.

![](img/5124daf79d2807d81e49f49c22f1f8c1_336_0.png)

## Figure 9.5 GNOME machine code for the 8-bit addition program.

The next instruction, load R0, has 0100 as the most-significant 4 bits of the encoding. The remaining 4 bits encode the address of the data RAM location. In this case that is RAM location zero, so the least-significant 4 bits are 0000 and the total opcode is 01000000.

As a final example, the instruction jump halt performs a program jump to the address labeled halt. The actual address associated with the label halt is seven (0000111 in 7-bit binary). The first bit of a jump instruction opcode is 1. The final 7 bits of the opcode is the address to jump to. So the opcode for the jump halt instruction is 10000111. That's all there is to it.

Once the opcodes are stored in the program memory, the GNOME can read out the bit patterns and execute the program. But what are the individual steps that must occur to execute each instruction? Each instruction has three basic steps:

Fetch: The GNOME must read the current instruction from the program memory and store it into the instruction register.

Decode: The GNOME must figure out which type of instruction is to be executed and get the required operands.

Execute: The GNOME must do the operation on the operands and store the result.

Table 9.3 shows these steps for each of the GNOME instructions. During the fetch step, a new instruction opcode is read from the address in the external RAM that is pointed to by the PC. This opcode is stored in the instruction register (IR). The program counter is also incremented so that it points to the next instruction (since all the GNOME instructions are 1 byte long).

During the decode step, the instructions will require different operations depending upon their addressing mode. For example, an instruction that uses direct addressing, like add Rd, first needs to get its data from memory. This is done by accessing the external memory with the memory address stored in the lower four bits of the opcode. The four-bit value read from memory replaces these address bits in the instruction register. On the other hand, immediate mode instructions like the load immediate data instruction (load #d) don't do anything during the decoding step because they already have their operands.

In the final execute step, the instruction is completed. To continue the description of the direct add instruction, the accumulator is loaded with the sum of the operand data (stored in the lower 4 bits of the IR), the current value in the accumulator, and the carry flag. As another example, the store Rd instruction stores the value in the accumulator into the memory location whose address is stored in the lower 4 bits of the opcode. Finally, the skip_c and skip_z instructions will increment the PC again (which will jump over the next instruction after the skip instruction) if the C or Z flag is set, respectively.
