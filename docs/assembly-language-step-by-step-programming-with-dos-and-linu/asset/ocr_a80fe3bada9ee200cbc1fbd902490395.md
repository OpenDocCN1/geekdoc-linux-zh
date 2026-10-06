We need to test them, we don't know what they are.) With the initial
value of 9DH, bit 4 turns out to be a 1, and bit 5 turns out to be a 0. If the
initial value was something else, bit 4 and 5 could both be 0, both
1, or some combination of the two.

Don't forget: The result of the AND operation replaces the first operand
after the operation is complete.

For an example of the AND instruction in operation isolating bits in a
word, look ahead to the Byte2Str procedure, which follows later in this
chapter.

# The OR Instruction

Closely related to the AND logical operation is OR, which, like the AND
logical operation, has an embodiment with the same name in the x86
instruction set. Structurally, the OR instruction works identically to
AND. Only its truth table is different: While AND requires that both
operands be 1 for the result to be 1, OR is satisfied that at least one
operand has a 1 value. The truth table for OR is shown in Table 10.3.

Because it's unsuitable for isolating bits, OR is used much more rarely
than AND.

# The XOR Instruction

A class by itself is the Exclusive OR operation, embodied in the XOR
instruction. XOR, again, does in broad terms what AND and OR do: It
performs a logical operation on two operands, and the result replaces
the first operand. The logical operation, however, is exclusive or, mean-
ing that the result is only 1 if the two operands are different (that is, 1 and
0 or 0 and 1). The truth table for XOR (Table 10.4) should make this slip-
yotion a little clearer.

Table 10.3 The OR Truth Table for Assembly Language
| BIT 1 | OPERATOR | BIT 2 | RESULT BIT |
|---|---|---|---|
| 0 | OR | 0 | 0 |
| 0 | OR | 1 | 1 |
| 1 | OR | 0 | 1 |
| 1 | OR | 1 | 1 |