```
OR AL, 80H ; Mask out bit 4.
OUT [70H], AL ; Write altered byte back out.
```

# 10.4 Shift Instructions

Registers which can shift bits right or left are called *shift registers*. Suppose that a 16-bit shift register contains the binary number

```
0110 1011 0011 1111
```

Shifting this number to the right by one bit yields

```
0011 0101 1001 1111
```

and sets the carry flag, since the rightmost bit was 1. Shift registers are part of the standard repertoire of microprocessors. In the x86, the bit which is "lost" is generally stored in the carry flag. Hence following the shift just shown, the carry flag would be set. Where the "new" bit comes from depends on which shift command is used. When the new bit is 0, the shift is referred to as a *logical shift*. Notice that shifting the number 6

```
0110
```

to the right by one bit in this manner

```
0011
```

yields 3. A rightward shift may thus be used to accomplish division by two. The logical shift, however, fails to do this correctly on signed numbers. An eight-bit two's complement value such as -4

```
1111 1100
```

when shifted to the right by one using a logical shift

```
0111 1110
```

yields 126, not -2. If what we really want is to divide by two, then the new leftmost bit should be copied from the old one. In this case we would get

```
1111 1110
```

instead, which actually is –2. This kind of a shift is referred to as an *arithmetic shift*, or sometimes also as a *sign-extended shift*. Since an arithmetic shift produces an erroneous division when a large unsigned value is used, the latter term is a probably better one. The problem does not occur with leftward shifts. The commands for rightward logical and arithmetic shifts are

```
SHR reg, imm
SHR reg, CL
SAR reg, imm
SAR reg, CL
```

where the immediate value must be a one-byte number. Leftward shifts use the mnemonics `SHL` and `SAL`. These two mnemonics actually refer to the same opcodes. They have the same valid forms as `SHR` and `SAR`. In all these cases, a memory operand may replace the register operand.

When the "lost" bit is recycled as the "new" bit, the shift is referred to as a *rotate*. `ROL` and `ROR` are mnemonics for rotate left and rotate right. Just as in the logical and arithmetic shifts, the carry flag takes on the value of the rotated bit. But it does not participate in the rotation. To include the carry bit into the cycle, use the `RCR` and `RCL` commands. `RCL` and `RCR` refer to rotate through carry left and rotate through carry right. Table 10.1 illustrates the effect of each of these rotate instructions, assuming that before the rotate