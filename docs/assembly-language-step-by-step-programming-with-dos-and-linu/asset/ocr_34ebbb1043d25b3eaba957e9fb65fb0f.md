# Pop Top of Stack into Operand

# Flags affected:

O D I T S A P C OF: Overlow flag TF: Trap flag AF: Aux carry
F F F F F F F DF: Direction flag SF: Sign flag PF: Parity flag
<none> IF: Interrupt flag ZF: Zero flag CF: Carry flag

# Legal forms:

+   - POP r16
- POP m16
- POP r32
- POP m32
- POP sr

# Examples:

+   - POP WORD [BX]
- POP EAX
- POP DX
- POP DWORD [EAX+ECX]
- POP ES

# Notes:

It is impossible to pop an 8-bit item from the stack. Also remember that the top of the stack is defined (in 16-bit modes) as the word at address SS:SP, and there's no way to override that using segment prefixes. In 32-bit modes, the top of the stack is the DWORD at [ESP]. There is a separate pair of instructions, PUSH and POPF, for pushing and popping the Flags register.

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