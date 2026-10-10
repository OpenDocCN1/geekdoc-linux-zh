instructions. For example, the mnemonic for a branch instruction is simply B. If we want to save a return address, called a branch and link instruction, the mnemonic is B, L. The L is a computer to the branch instruction. Similarly, the store word instruction, STW, can become a store word and modify with a computer of  M : STW, M.

Some tools will also use simplified mnemonics. The branch and link instruction is used to call a procedure, so it is sometimes shown in a listing as a CALL instruction. As another example, there is no “no operation” instruction in PA-RISC, but the assembler will use OR 0,0,0 as a no-op, and this instruction is frequently decoded as NOP in assembly listings.

# ### Memory Reference Instructions

The PA-RISC architecture uses explicit LOAD and STORE operations for all memory access. LOAD instructions bring data from memory to registers, and STORE instructions move data from registers to memory. Since PA-RISC uses memory-mapped I/O, the LOAD and STORE instructions are also used for all I/O operations. There are no explicit I/O operations in the instructions set.

LOADs and STOREs can operate on a byte, a halfword, a word, or a doubleword. These instructions are summarized in Table 2-1.

**Table 2-1 LOAD and STORE Instructions**

| Size of Operand | Load Instruction | Store Instruction |
|---|---|---|
| 8 bits | LDB – Load byte | STB – Store byte |
| 16 bits | LDH – Load halfword | STH – Store halfword |
| 32 bits | LDW – Load word | STW – Store word |
| 64 bits | LDD – Load doubleword | STD – Store doubleword |

The most common addressing mode for memory uses a *base register* and a *displacement* to specify the target address. The displacement is added to the contents of the register to get the target address. The data at that address is then copied to the specified register (for a LOAD), or the contents of the register are copied to that address (for a STORE). An example is the instruction

```
LDW 4(r31),r27
```

This instructs the system to add 4 to the value in GR31, use the resulting sum as an address into memory, and load the value from that address into GR27. This base and displacement technique is frequently used for referencing members of a structure through a pointer—a common operation in the kernel. Consider the following code sample:

```
struct mysttruct {
	int	x;	/* 32 bit integers */
	int	y;
}
```