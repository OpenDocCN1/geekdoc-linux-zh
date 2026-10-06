# CLD Clear Direction Flag (DF)

Flags affected:

O D I T S Z A P C OF: Overflow flag TF: Trap flag AF: Aux carry
F F F F F F F F DF: Direction flag SF: Sign flag PF: Parity flag
* IF: Interrupt flag ZF: Zero flag CF: Carry flag

Legal forms:

```
CLD <none>
```

Examples:

```
CLD
```

Notes:

CLD simply sets the Direction flag (DF) to the cleared (0) state. This affects the adjustment performed by repeated string instructions such as STOS, SCAS, and MOVS. Typically, when DF = 0, the destination pointer is increased, and decreased when DF = 1. is set to one with the STD instruction.

```
r8 = AL AH BL BH CL CH DL DH r16 = AX BX CX DX BP SP SI DI
sr = CS DS SS ES FS GS               r32 = EAX EBX ECX EBP ESP ESI EDI
m8 = 8-bit memory data             m16 = 16-bit memory data
m32 = 32-bit memory data             i8 = 8-bit immediate data
i16 = 16-bit immediate data         i32 = 32-bit immediate data
d8 = 8-bit signed displacement     i16 = 16-bit signed displacement
d32 = 32-bit unsigned displacement
```