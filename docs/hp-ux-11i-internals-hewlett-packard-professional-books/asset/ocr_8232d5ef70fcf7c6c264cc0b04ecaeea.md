| Condition | Definition |
| --- | --- |
| >= | Operand 1 is greater than or equal to negative of operand 2 (signed) |
| > | Operand 1 is greater than negative of operand 2 (signed) |
| UV | Operand 1 plus operand 2 overflows (unsigned) |
| VNZ | Operand 1 plus operand 2 is nonzero and overflows (unsigned) |
| NSV | Operand 1 plus operand 2 does not overflow (signed) |
| EV | Operand 1 plus operand 2 is even |

As an example, consider the instruction ADDIB, OD 17,r4,main+0x18. The value 17 is added to the contents of GR4, and the result is placed in GR4. If the result is odd, then the branch to main+0x18 will be taken.

The branch on bit instruction examines a bit in a register and conditionally branches based on that bit. The arguments to the instruction are the register, the position of the bit, and the target address. Table 2-7 lists the possible conditions for the BB instruction. The position argument can be a fixed bit position, or it can be SAR, which refers to the Shift Amount Register (CR11).

| Condition | Definition |
| --- | --- |
| < | Leftmost bit in word is 1 |
| >= | Leftmost bit in word is 0 |

# ## Delayed Branching

All branching in PA-RISC uses a feature known as delayed branching. This means that the instruction immediately following the branch will be executed even if the branch is taken. This instruction following a branch is called the delay slot. Consider the following code:

```
LDW0x20(x30), r2
COMIB,>10,r2,main+80
LDW0x24(x30), r3
```

The first instruction loads the value from 0x20 past GR30 into GR2. Next, the compare instruction compares that value to 10 and branches to main+80 if GR2 < 10. The next LDW