NASM allows use of the segmentwide form by inserting the NEAR keyword after the instruction mnemonic. In real mode this allows the use of a 16-bit signed displacement, and in 32-bit protected mode this allows the use of a 32-bit signed displacement. Use of NEAR is only supported with 386 and newer CPUs.

```
r8 = AL AH BL BH CL DL DH    r16 = AX BX CX DX BP SP SI DI
sr = CS DS SS ES FS GS          r32 = EAX EBX ECX EBP ESP ESI EDI
m = 8-bit memory data             m16 = 16-bit memory data
m32 = 32-bit memory data         i8 = 8-bit immediate data
i16 = 16-bit immediate data     i32 = 32-bit immediate data
d8 = 8-bit signed displacement  d16 = 16-bit signed displacement
d32 = 32-bit unsigned displacement
```