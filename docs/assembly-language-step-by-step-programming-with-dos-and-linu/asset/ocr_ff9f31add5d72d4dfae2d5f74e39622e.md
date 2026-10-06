# XOR Exclusive Or

Flags affected:

O D I T S Z A P C OF: Overflow flag TF: Trap flag AF: Aux carry
F F F F F F F F DF: Direction flag SF: Sign flag PF: Parity flag
* * * * * * * * IF: Interrupt flag ZF: Zero flag CF: Carry flag

# Legal forms:

```
XOR r8,r8
XOR m8,r8
XOR r8,m8
XOR r16,r16
XOR m16,r16
XOR r16,m16
XOR r32,r32 386+
XOR m32,r32 386+
XOR r32,m32 386+
XOR r8,i8
XOR m8,i8
XOR r16,i16
XOR m16,i16
XOR r32,i32 386+
XOR m32,i32 386+
XOR AL,i8
XOR AX,i16
XOR EAX,i32 386+
```

# Examples:

```
XOR BX,DI ;Uses single-byte opcode
XOR AX,0FFFF ;Uses single-byte opcode
XOR AL,42H
XOR EBX, DWORD [EDI]
XOR WORD [ES:BX],0B00H
XOR WORD [BX+SI],DX
```

# Notes:

XOR performs the exclusive OR operation between its two operands. Once the operation is complete, the result replaces the destination operand. XOR is performed on a bit-by-bit basis, such that 0 of the source is XORed with 0 of the destination, and 1 with 1. XOR yields a 1 if the operands are different, and so on. Note that the operation sets the Auxiliary carry flag undefined. CF and OF are cleared to 0, and other affected flags are set according to the operation’s results.

```
r8 = AL BH BL CH DL DH r16 = AX BX CX DX BP SI DI
sr = CS DS FS GS r32 = EAX EBX EDX EBP ESI EDI
m8 = 8-bit immediate data m16 = 16-bit immediate data
m32 = 32-bit memory data i18 = 8-bit immediate data
i16 = 16-bit immediate data i32 = 32-bit immediate data
d8 = 8-bit signed displacement d16 = 16-bit signed displacement
d32 = 32-bit unsigned displacement
```