# # Notes on the Instruction Set Reference

# ## Instruction Operands

When an instruction takes two operands, the destination operand is the one on the left, the source operand is the one on the right. In general, when a result is produced by an instruction, the result replaces the destination operand. For example, in this instruction:

```
ADD BX, SI
```

the BX register is added to the SI register, and the sum is then placed in the BX register, overwriting whatever was in BX before the addition.

# ## Flag Results

Each instruction contains a flag summary that looks like this (the asterisks will vary from instruction to instruction):

```
O D I T S Z A P C Overflow flag TF: Trap flag AF: Aux carry
F F F F F F F DF: Direction flag SF: Sign flag PF: Parity flag
* * * * * * IF: Interrupt flag ZF: Zero flag CF: Carry flag
```

The nine flags are all represented here. An asterisk indicates that the instruction on page affects that flag. If a flag is affected at all (that, if it has an asterisk beneath it), it will be affected by these rules:

+   - OF Set the result is too large to fit in the destination operand.
- IF Set by the STI instruction; cleared by CLI.
- TF For debuggers; not used in normal programming and may be ignored.
- SF Set when the sign of the result forces the destination operand to become negative.
- ZF Set if the result of an operation is zero. If the result is nonzero, ZF is cleared.
- AF Auxiliary carry used for 4-bit BCD math. When an operation causes a carry out of a 4-bit BCD quantity.
- PF Set if the number of 1 bits in the low byte of the result is even; cleared if the number of 1 bits in the low byte of the result is odd. Used in data communications applications but little else.
- CF Set if the result of an add or shift operation carries out a bit