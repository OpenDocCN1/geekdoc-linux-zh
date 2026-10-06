
# MOV Move (Copy) Right Operand into Left Operand

Flags affected:

```
O D I T S Z A P C  OF: Overflow flag TF: Trap flag AF: Aux carry
F F F F F F F DF: Direction flag SF: Sign flag PF: Parity flag
<none>           IF: Interrupt flag ZF: Zero flag CF: Carry flag
```

# Legal forms:

```
MOV r8,r8
MOV m8,r8
MOV r8,m8
MOV r8,i8
MOV m8,i8
MOV r16,r16
MOV m16,r16
MOV r16,m16
MOV m16,i16
MOV r16,i16
MOV r32,r32    386+
MOV m32,r32    386+
MOV r32,m32    386+
MOV r32,i32    386+
MOV m32,i32    386+
MOV sr,r16
MOV sr,m16
MOV r16,sr
MOV m16,sr
```

# Examples:

```
MOV AL, BH
MOV EBX, EDI
MOV BP, ES
MOV ES, AX
MOV AX,0B00H
MOV ES: [BX],0FFFFH
MOV CX, [SI+Offset]
```

# Notes:

This perhaps the most used of all instructions. The flags are not affected.

```
r8 = AL AH BH BL CL LD DH  r16 = AX BX CX DX BP SP SI DI
sr = CS DS SS ES FS GS          r32 = EAX EBX ECX EDX EBP ESP EDI
m8 = 8-bit memory data        m16 = 16-bit memory data
m32 = 32-bit memory data      i8 = 8-bit immediate data
i16 = 16-bit immediate data   i32 = 32-bit immediate data
d8 = 8-bit signed displacement  d16 = 16-bit signed displacement
d32 = 32-bit unsigned displacement
```

# Negate (Two’s Complement; i.e., Multiply by -1)

Flags affected:

O D I T S Z A P C OF: Overflow flag TF: Trap flag AF: Aux carry
F F F F F F F DF: Direction flag SF: Sign flag PF: Parity flag
* * * * * * * * IF: Interrupt flag ZF: Zero flag CF: Carry flag

Legal forms:

```
NEG r8
NEG m8
NEG r16
NEG m16
NEG r32      386+
NEG m32      386+
```

# Examples:

```
NEG AL
NEG DX
NEG ECX
NEG BYTE [BX]    ; Negates BYTE quantity at [BX]
NEG WORD [DI]    ; Negates WORD quantity at [DI]
NEG DWORD [EAX]  ; Negates DWORD quantity at [EAX]
```

# Notes:

This is the assembly language equivalent of multiplying a value by -1. Keep in mind that negation is not the same as simply inverting each bit in the operand. (Another instruction, NOT, does that.) The process is also known as generating the two’s complement of a value. The two’s complement of a value added to that yields zero. -1 = FF; -2 = FE; -3 = FD; and so forth.

If the operand is 0, CF is cleared and ZF is set; CF is set and ZF is cleared. If the operand contains the maximum negative value (-128 for 8-bit or -32,768 for 16-bit), the operand does not change, but OF and CF are set. If the result is negative, or else SF is cleared. PF is set if the lower-order 8 bits of the result contain an even number of set (1) bits; otherwise, PF is cleared.

You use a size specifier (BYTE, WORD, DWORD) with memory data:

```
r8 = AL AH BH BH CL DH DI      r16 = AX BX CX DX BP SI DI
sr = CS DS ES SS FS SS          r32 = EAX EBX ECX EDX ESP ESI EDI
m8 = 8-bit memory data        m16 = 16-bit memory data
m32 = 32-bit memory data      i8 = 8-bit immediate data
i16 = 16-bit immediate data   i32 = 32-bit immediate data
d8 = 8-bit signed displacement  d16 = 16-bit signed displacement
d32 = 32-bit unsigned displacement
```

# NOP No Operation

Flags affected:

O D I T S Z A P C OF: Overflow flag TF: Trap flag AF: Aux carry
F F F F F F DF: Direction flag SF: Sign flag PF: Parity flag
<none> IF: Interrupt flag ZF: Zero flag CF: Carry flag

# Legal forms:

NOP <none>

# Examples:

NOP

# Notes:

This, the easiest-to-understand of all 86-family instructions, simply nothing. Its job is to take up space in sequences of instructions. When fetched by the CPU, NOP is executed as XCHG AX,AX. So, some work is actually done, but not useful, and no data is altered. The flags are not affected. NOP is used for debugging, leaving space for future calls, or timing loops.

```
r8 = AL AH BH BH CL DL DH          r16 = AX BX CX DX BP SI DI
sr = CS DS SS ES FS GS r32 = EAX EBX ECX EDX ESP EDI
m8 = 8-bit memory data i8 = 8-bit immediate data
m32 = 32-bit memory data i32 = 32-bit immediate data
i16 = 16-bit immediate data d16 = 16-bit signed displacement
d8 = 8-bit signed displacement
d32 = 32-bit unsigned displacement
```

# Logical NOT (One's Complement)

Flags affected:

O D I T S Z A P C OF: Overflow flag TF: Trap flag AF: Aux carry
F F F F F F DF: Direction flag SF: Sign flag PF: Parity flag
<none> IF: Interrupt flag ZF: Zero flag CF: Carry flag

# Logical forms:

NOT r8
NOT m8
NOT r16
NOT m16
NOT r32 386+
NOT m32 386+

# Examples:

NOT CL
NOT DX
NOT EBX
NOT WORD [SI+Offset]

# Notes:

NOT inverts each bit within the operand separately. That is, every bit that was 1 becomes 0, and every bit that 0 becomes 1. This is the “logical NOT” or “one’s complement” operation. See the NEG instruction for the negation, or two’s complement operation. After execution of NOT, the value FFH would become 0; the value AAH would become 55H. You must use a size specifier (BYTE, WORD, DWORD) with memory data!

```
r8 = AL AH BH CL DL DH          r16 = AX BX CX DP SI DI
SR = CS DS SS ES FS GS             r32 = EAX ECX EDX ESP EDI
m8 = 8-bit memory data             m16 = 16-bit memory data
m32 = 32-bit memory data          i8 = 8-bit immediate data
i16 = 16-bit immediate data      i32 = 32-bit immediate data
d8 = 8-bit signed displacement  d16 = 16-bit signed displacement
d32
```

# OR Logical OR

Flags affected:

O D I T S Z A P C OF: Overflow flag TF: Trap flag AF: Aux carry
F F F F F F F DF: Direction flag SF: Sign flag PF: Parity flag
* * * * * * * IF: Interrupt flag ZF: Zero flag CF: Carry flag

Logical forms:

OR r8,r8
OR m8,r8
OR r8,m8
OR r16,r16
OR m16,r16
OR r16,m16
OR r32,r32 386+
OR m32,r32 386+
OR r32,m32 386+
OR r8,i8
OR m8,i8
OR r16,r16
OR m16,i16
OR r32,i32 386+
OR m32,i32 386+
OR AL,i8
OR AX,i16
OR EAX,i32 386+

Examples:

OR EBX, EDI ;Uses single-byte opcode
OR AX, 0FFFF ;Uses single-byte opcode
OR AL, 42H
OR WORD [ES:BX],0B800H
OR WORD [BP+SI],DX

Notes:

OR performs the OR logic operation between its operands. Once the operation is complete, the result replaces the destination operand. OR is performed on a bit-by-bit basis, such that 1 of the source is ORed with 0 of the destination, 1 of the source is ORed with 1 of destination, and so on. The operation yields a 1 if one of the operands is 1, and 0 only if both operands are 0. The operation makes the Auxiliary flag cleared, and the affected flags are set according to results. Note: You must use a size specifier (BYTE, WORD, DWORD) with memory data:

```
r8 = AL AH BH BH CL DH DI      r16 = AX BX CX DX BP SI DI
sr = CS DS ES SS FS SS          r32 = EAX EBX ECX EDX ESP ESI EDI
m8 = 8-bit memory data        m16 = 16-bit memory data
m32 = 32-bit memory data      i8 = 8-bit immediate data
i16 = 16-bit immediate data   i32 = 32-bit immediate data
d8 = 8-bit signed displacement  d16 = 16-bit signed displacement
d32 = 32-bit unsigned displacement
```

# Pop Top of Stack into Operand

Flags affected:

O D I T S Z A P C OF: Overflow flag TF: Trap flag AF: Aux carry
F F F F F F F DF: Direction flag SF: Sign flag PF: Parity flag
<none> IF: Interrupt flag ZF: Zero flag CF: Carry flag

# Legal forms:

+ - POP r16
- POP m16
- POP r32
- POP m32
- POP sr

# Examples:

+ - POP WORD [BX]
- POP EAX
- POP DX
- POP DWORD [EAX+ECX]
- POP ES

# Notes:

It is impossible to pop an 8-bit item from the stack. Also remember that the top of the stack is defined (in 16-bit modes) as the word at SS:SP, and there's no way to override that using segment prefixes. In 32-bit modes, the top of the stack is the DWORD at [ESP]. There is a separate pair of instructions, PUSH and POPF, for pushing and popping the Flags register.

All register forms have single-byte opcodes. NASM recognizes them and generates them automatically, even though there are larger forms in the CPU instruction decoding logic.

```
r8 = AL AH BH BH CL DL DH          r16 = AX BX CX DX BP SP SI DI
sr = CD CD DS SS FS FS GS             r32 = EAX EBX ECX EDX EBP ESP EDI
m8 = 8-bit memory data             m16 = 16-bit memory data
m32 = 32-bit memory data            i8 = 8-bit immediate data
i16 = 16-bit immediate data          i32 = 32-bit immediate data
d8 = 8-bit signed displacement      d16 = 16-bit signed displacement
d32 = 32-bit unsigned displacement
```
