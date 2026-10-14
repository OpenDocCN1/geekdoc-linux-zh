
Once it is compiled, the VHDL version of the FIFO will respond to the same XSPORT command sequences as the ABEL version does.

## Projects

- 1. Design the largest 4-bit-wide memory that you can in a single FPLD using just flip-flops and gates.
- 2. Design the largest 4-bit-wide memory that you can with the internal RAM of the XC4005XL.
- 3. Design a 7-segment LED decoder using only the internal RAM and the fact that the RAM can be loaded when the XC4005XL is configured.
- 4. Modify the FIFO design so that the prevop0 flip-flop output is used in place of the prevop1 output. Compile, download, and test the design. What happens?
- 5. Modify the FIFO design so that the multiplexer will output the rdptr instead of the wrptr when no operation is occurring. Compile, download, and test the design. What happens?
- 6. Increase the size of the FIFO from 16 to 32768. How much of the FPLD is used now?
- 7. Replace the external RAM with the internal memories of the XC4005XL. How do you handle the interface to the RAM data input and output buses? Does the new design perform equivalently to the original?
- 8. Use a dual-port RAM to build the FIFO so that simultaneous reads and writes can occur.

## The GNOME Microcomputer

## Objectives

- Discuss the programmer's model for the GNOME microcomputer.
- Show how to program the GNOME.
- Explain the process of binary multiplication.
- Describe the general organization of the GNOME.
- Show how to build the controller section of the GNOME.
- Show how to build the circuitry of the GNOME datapath.
- Show how the GNOME controller and the datapath work together.

## Discussion

You have seen how a RAM is built, but you may be asking, "Why are large memories needed?" After all, the largest memory you have needed so far is only a few bits for storing the state of some of your state machines. Some of you may be replying, "It's obvious why we need large RAMs—they are for storing large amounts of data!" Of course, you are right—RAMs are good for storing large amounts of data.

But just having a memory to store data is rather useless. Imagine having all the data on every purchase made by every person in the United States over the course of a year. Now suppose you want to find the group of people who have purchased Volvos so you can sell them a horn that yodels instead of beeps. Your only recourse is to address each memory location and pick out the data you need (and we are talking trillions of memory locations).

However, you could write down detailed instructions and give them to someone else and tell them to find the information you want. These instructions constitute a program and the paper they are written on is a primitive memory. If you had a way to encode the written instructions as binary numbers, you could store them in a RAM just like the data. Then you could build a state machine to interpret the binary numbers stored in the program RAM (which are called

Figure 9.2 Adding two 8-bit numbers using a 4-bit ALU.

The two 8-bit numbers to be added are 0x48 and 0x29 (these numbers are in hexadecimal). All the data memory in the GNOME is 4 bits wide. A 4-bit number is called a nybble. An 8-bit number (or byte) can only be stored by using two memory locations in the data RAM: one for the least-significant nybble (LSN) and one for the most-significant nibble (MSN) (see Figure 9.3). Let's assume that the MSN of 0x48 (which is 4) is stored in register R1 of the data RAM and the LSN is stored in R0. The second operand is stored similarly, with the MSN placed in R3 and the LSN placed in R2. The 8-bit result of adding these two numbers will be stored in R5 (MSN) and R4 (LSN).

![](img/5124daf79d2807d81e49f49c22f1f8c1_327_0.png)

# Figure 9.3 The arrangement of bits and nybbles in a byte.

Upon startup, the program RAM is already loaded with the instruction opcodes and the PC is initialized to 0 so it points to the first instruction (Figure 9.2a). (In the figure, the instruction mnemonic is shown instead of the binary opcode in order to make the execution of the program easier to understand.) The operands are already stored in R0, R1, R2, and R3. The RAM for the result, however, is not initialized and contains some random number (represented by ?). The accumulator is also not initialized, and neither are the carry or zero flags. The carry flag acts as both the input carry bit to the ALU and stores the output carry after the ALU adds two 4-bit numbers. For this program, you want to start with C = 0. The clear_c instruction clears the carry bit. Note that in Figure 9.2b the carry bit is now zero and the PC has been incremented so it points to the next instruction.

The next instruction, load R0, is used to load the LSN of the first operand into the accumulator. In effect, the instruction mnemonic means "load the value found in R0 into the ACC." Note that while the address of the RAM location that holds the data (R0) is explicitly mentioned, the place where the data is transferred to (ACC) is only implied. After executing this instruction, the ACC holds the value 0x8 and the PC has been incremented.

The next instruction (Figure 9.2c) is add R2, which you might guess would be an instruction to add the contents of R2 to something. But what? Again, the implied operand is the accumulator. This instruction actually means "add the value found in R2, the value in the ACC, and the bit in the C flag, and store the result in the ACC while loading the C flag with the carry output." In this case, the result (in both hexadecimal and binary representations) will be:
