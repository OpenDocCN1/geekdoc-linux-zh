# BT Test (386+)

# Flags affected:

O D I T S Z A P C OF: Overflow flag TF: Trap flag AF: Aux carry
F F F F F F F F DF: Direction flag SF: Sign flag PF: Parity flag
IF: Interrupt flag ZF: Zero flag CF: Carry flag

# Legal forms:

+   - BT r16,r16 386+
- BT m16,r16 386+
- BT r32,r32 386+
- BT m32,r32 386+
- BT r16,18 386+
- BT m16,18 386+
- BT r32,18 386+
- BT m32,18 386+

# Examples:

+   - BT AX,CX
- BT [BX-DI],DX
- BT AX,64
- BT EAX,EDX
- BT ECX,17

# Notes:

BT copies a single bit from the left operand to the Carry flag, where it can be tested or a quantity using the shift/rotate instructions. Which bit is copied is fed back into the right operand. Neither operand is altered by BT.
When the right operand is an 8-bit immediate value, the value specifies the number of bit to be copied. In BT AX,5 5 of AX is copied into CF. If the immediate value exceeds the size of the left operand, the value is expressed modulo the size of the left operand. That is, because there are not 66 bits in EAX, EAX,66 pulls out all 32s from the immediate value as be taken, and what remains is the number. (Here, 2) When the right operand is not an immediate value, the right operand not only specifies the bit to be tested also an offset from the memory reference in the left operand. This is complicated. See a detailed discussion in a full assembly language reference.

```
r8 = AL AH BL CH CL DL DH          r16 = AX CX DX BX BP SP SI
sr = CS DS SS ES BH FS GS            EAX = EAX EBX ECX EBP ESP ESI EDI
m8 = 8-bit memory data               m16 = 16-bit memory data
m32 = 32-bit memory data             i8 = 8-bit immediate data
i16 = 16-bit immediate data        i32 = 32-bit immediate data
d8 = 8-bit signed displacement      d16 = 16-bit signed displacement
d32 = 32-bit unsigned displacement
```