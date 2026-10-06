# PUSHA Push All 16-Bit GP Registers (286+)

# Flags affected:

O D I T S Z A P C OF: Overflow flag TF: Trap flag AF: Aux carry
F F F F F F F DP: Direction flag SF: Sign flag PF: Parity flag
<none> IF: Interrupt ZF: Zero flag CF: Carry flag

# Legal forms:

PUSHA 286+

# Examples:

PUSHA

# Notes:

PUSHA pushes all 16-bit general-purpose registers onto the stack. This instruction is present on the 286 and later CPUs and is not available in the 8086/8088.

The registers are pushed in this order:

AX, CX, DX, BX, SP, BP, SI, DI

However, note that the value of SP pushed is the value SP had before the first register was pushed onto the stack. In the course of executing PUSHA, the stack pointer is decremented by 16 bytes (8 registers x 2 bytes each).

The Flags is not pushed onto the stack by PUSHA; see PUSHF.

```
r8 = AL AH BL BH CH DL DH          r16 = AX CX DX BP SP SI DI
sr = CD DS SS ES FS GS                   r32 = EAX EDX ECX EBP ESI EDI
m8 = 8-bit memory data                 m16 = 16-bit memory data
m32 = 32-bit memory data              i18 = 8-bit immediate data
i16 = 16-bit immediate data          i32 = 32-bit immediate data
d8 = 8-bit signed displacement       d16 = 16-bit signed displacement
d32 = 32-bit unsigned displacement
```