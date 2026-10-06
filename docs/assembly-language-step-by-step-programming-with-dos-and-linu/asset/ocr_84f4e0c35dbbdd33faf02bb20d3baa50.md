# Partial 8086/8088 Instruction Set Reference 583

# SHL Shift Left

Flags affected:

```
O D I T S Z A P C OF: Overflow flag TF: Trap flag AF: Aux carry
F F F F F F F F DF: Direction flag SP: Sign flag PF: Parity flag
* * * * * * IF: Interrupt flag ZF: Zero flag CF: Carry flag
```

# Legal forms:

```
SHL r8,1
SHL m8,1
SHL r16,1
SHL m16,1
SHL r32,1    386+
SHL m32,1    386+
SHL r8, CL
SHL m8, CL
SHL r16, CL
SHL m16, CL
SHL r32, CL    386+
SHL m32, CL    386+
SHL r8,i8    286+
SHL m8,i8    286+
SHL r16,i8   286+
SHL m16,i8   286+
SHL r32,i8   386+
SHL m32,i8   386+
```

# Examples:

```
SHL AL, 1
SHL WORD [BX+SI], CL
SHL BP, 1
SHL EAX, 9
SHL BP, CL
```

# Notes:

SHL shifts the bits within the destination operand to the left, where left is toward the most significant bit (MSB). The number of bit positions shifted may be specified either as an 8-bit immediate value, or by the value in CL—not CX or ECX (The 8086 and 8088 are limited to the immediate value 1). Note that CL may accept a value up to 255, it means impossible to shift by any value larger than 16—or 32 in 32-bit mode—even though the shifts are actually performed on the 8086 and 8088 (The 286 and later limit the number of shift operations performed to the word size except when running in Virtual 86 mode). The leftmost bit of the order is shifted into the Carry flag; the rightmost bit is cleared to 0. The Auxiliary carry flag (AF) becomes undefined after this instruction. OF is modified only by the shift-by-one forms of SHL; after shift-by-CL forms, OF becomes undefined.