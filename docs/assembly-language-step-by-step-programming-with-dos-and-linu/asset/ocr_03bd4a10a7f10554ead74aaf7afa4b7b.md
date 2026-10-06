# OR Logical OR

Flags affected:

O D I T S Z A P C OF: Overflow flag TF: Trap flag AF: Aux carry
F F F F F F F F DF: Direction flag SF: Sign flag PF: Parity flag
* * * * * * * * IF: Interrupt flag ZF: Zero flag CF: Carry flag

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
OR r16,i16
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

OR performs the OR logic operation between its operands. Once the operation is complete, the result replaces the destination operand. OR is performed on a bit-by-bit basis, such that 1 of the source is ORed with 0 of the destination, 1 of the source is ORed with 1 of destination, and so on. The operation yields a 1 if one of the operands is 1, and 0 only if both operands are 0. The operation makes the Auxiliary carry flag undefined. CF and OF are cleared to 0, and the affected flags are set according to the operation's results.

Note: You must use a sizeifier (BYTE, WORD, DWORD) with memory data:

```
r8 = AL AH BL BH CL DL DH      r16 = AX BX CX DX BP SP SI DI
sr = CS DS SS ES FS FS          r32 = EAX ECX EBP ESP ESI EDI
m8 = 8-bit memory data        m16 = 16-bit memory data
m32 = 32-bit memory data      i8 = 8-bit immediate data
i16 = 16-bit immediate data  m32 = 32-bit immediate data
d8 = 8-bit signed displacement  d16 = 16-bit signed displacement
d32 = 32-bit unsigned displacement
```