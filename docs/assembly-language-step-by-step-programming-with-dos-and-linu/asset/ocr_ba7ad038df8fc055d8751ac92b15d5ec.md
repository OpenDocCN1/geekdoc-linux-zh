# RET Return from Procedure

# Flags affected:

O D I T Z A P C OF: Overflow flag TF: Trap flag AF: Aux carry
F F F F F F F DF: Direction flag SF: Sign flag PF: Parity flag
<none> IF: Interrupt flag ZF: Zero flag CF: Carry flag

# Legal forms:

+   RET
RETN
RETF
RET i8
RETN i8
RET i16
RETF i16

# Examples:

+   RET
RET 12H
RETN
RETF 17H

# Notes:

There are two kinds of returns: Near and Far, where Near is within the current code segment and Far is to some other segment. Ordinarily, the RET form is used, and the assembler resolves it to a Near or FAR return opcode to match the procedure's definition using of the NEAR or FAR specifier. Specifying RETF or RETN may be done when necessary.

RET may take an operand indicating how many bytes of stack space are to be released on returning from the procedure. This figure is subtracted from the stack pointer to erase items that have been pushed onto the stack for the procedure's use immediately prior to the call.

The RET and RETN forms are not available in MASM after V5.0!

```
r8 = AL AH BH CH CL DH r16 = AX BX CX DX BP SI DI
sr = CS CS SI SI ES FS GS r32 = EAX EBX ECX EDX EBP ESP ESI EDI
m8 = 8-bit memory data m16 = 16-bit memory data
m32 = 32-bit memory data i8 = 8-bit immediate data
i16 = 16-bit immediate data i32 = 32-bit immediate data
d8 = 8-bit signed displacement d16 = 16-bit signed displacement
d32 = 32-bit unsigned displacement
```