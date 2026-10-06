Similarly, if IMUL uses a 16-bit operand, the results will be placed in DX:AX, even if the entire result will fit in AX! It's easy to forget that IMUL affects DX on 16-bit multiples, and EDX in 32-bit multiples. Keep that in mind!

In both the two- and three-operand forms, the product replaces the contents of the first operand. In the two-operand form, the two operands are multiplied together, and the product replaces the first operand. In this it is like most other arithmetic and logical instructions. In the three-operand form, the second and third operand are multiplied, and the product replaces the first operand.

Note that with the two- and three-operand forms, there is the possibility that the product will not entirely fit in the destination register. When using those forms, the CF and OF flags will both be 0 (cleared) if the product fits entirely in the destination. It's best to use the original forms in cases where you aren't sure of the range the product might take.

```
r8 = AL AH BL BH CL CH DL DH             r16 = AX BX CX DX BP SP SI DI
sr = CS DS SS ES FS GS               r32 = EAX EBX ECX EDX EBP ESI EDI
m8 = 8-bit memory data                 m16 = 16-bit memory data
m32 = 32-bit memory data                 i8 = 8-bit immediate data
i16 = 16-bit immediate data           i32 = 32-bit immediate data
d8 = 8-bit signed displacement       d16 = 16-bit signed displacement
d32 = 32-bit unsigned displacement
```