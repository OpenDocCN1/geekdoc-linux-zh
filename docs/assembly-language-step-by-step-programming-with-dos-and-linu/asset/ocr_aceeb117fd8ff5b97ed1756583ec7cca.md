Partial 8086/8088 Instruction Set Reference

# IRET Return from Interrupt

Flags affected:

```
* D I T S Z A P C OF: Overflow flag TF: Trap flag AF: Aux carry
* F F F F F F F DF: Direction flag SF: Sign flag PF: Parity flag
* * * * * * * * IP: Interrupt flag ZF: Zero flag CF: Carry flag
```

# Legal forms:

```
IRET
```

# Examples:

```
IRET
```

# Notes:

IRET must be used to exit from interrupt service routines called through INT or interrupt hardware such as serial ports and the like. IRET pops the return address from the top of the stack into CS and IP, and then pops the next word from the stack into the Flags register. All flags are affected.

If the interrupt was triggered by hardware, there may be additional steps to be taken to prepare the hardware for another interrupt before IRET is executed. Consult your hardware-documentation.

When using NASM, the actual opcode generated for IRET depends on the setting of the BITS setting, and governs whether a 16-bit return or 32-bit return is generated.

```
r8 = AL AH BH CH DL DH      r16 = AX BX CX DX BP SP ESI DI
sr = CD DS SS ES FS GS        r32 = EAX EBX ECX EDX EBP ESP ESI EDI
m8 = 8-bit memory data       m16 = 16-bit memory data
m32 = 32-bit memory data     i8 = 8-bit immediate data
i16 = 16-bit immediate data i32 = 32-bit immediate data
d8 = 8-bit signed displacement d16 = 16-bit signed displacement
d32 = 32-bit unsigned displacement
```