```
0000 0000 0000 0000 0000 0000 0001 0001
0000 0000 0000 0000 0000 0000 0001 0010
0000 0000 0000 0000 0000 0000 0001 0011
```

Note that these addresses differ only in the "non-existent" bottom two bits. These four bytes are actually just one four-byte word. The command can be accomplished with a single memory transfer. On the other hand the command

```
MOV EAX, [12H]
```

which also accesses four bytes of memory, cannot be carried out in the same way. The 32-bit addresses of these four bytes are

```
0000 0000 0000 0000 0000 0000 0001 0010
0000 0000 0000 0000 0000 0000 0001 0011
0000 0000 0000 0000 0000 0000 0001 0100
0000 0000 0000 0000 0000 0000 0001 0101
```

To access these four bytes, two distinct memory transfers are required. In code which is accessing a large number of consecutive memory locations, four bytes at a time, performance will be cut in half if the addresses called are not those whose bottom two bits are zero, i.e. a multiple of four. Memory transfers which straddle four-byte word boundaries are said to be *out of alignment*. Starting with the 486 processor, a flag was added which detects memory transfers that are out of alignment.

# 6.2 Addresses in Brackets

The use of MOV to access memory just scratches the surface of available memory commands. All of the entries in Table 5.2 containing operand keys that contain an **m** describe commands that access memory. From the table, we can see that MOV, ADD, OR, ADC, SBB, AND, SUB, and XOR all allow memory operands in either the source or the destination operand position. Memory operands may be supplied using several different formats.

# 6.2.1 The [imm] Format

All the memory operand examples presented so far have used the [imm] format with the MOV instruction. Illustrating the [imm] format with the ADD command we have both

```
ADD reg, [imm]
```

and

```
ADD [imm],reg
```

where **imm** can be any four-byte number.

As we all know, memory may be used for storage of many kinds of data, including text, graphics, and numbers. In the following paragraphs we look at how it is used in connection with numbers, in particular with big numbers.

# 64-Bit Arithmetic

Memory space is much larger than processor space. When numbers become too large for the processor to work with, the arithmetic can be done piecemeal, with pieces small enough for the processor to handle loaded in from memory as they are needed. Some features of the processor are designed with this kind of arithmetic in mind. The ADC instruction is a case in point. This instruction makes it possible to do piecemeal addition of large numbers. Suppose that we have the numbers 1111222233334444H and AAAABBBBCCCCDDDDH stored at locations 100H and 108H in memory, and that we want to add them. Using the ADD instruction on the bottom four bytes of these numbers will set the carry flag. Using the ADC instruction on the next four bytes takes account of the carry. The ADC instruction is very similar to the ADD