
## Unconditional Branch

Table 2-2 shows the types of unconditional branches. The external branches are used to branch to a location in a different space: the vectored branches branch to an address held in a register; and the link branches save the return address in a register.

### Table 2-2 Unconditional Branches

| Instruction | Definition |
| :--- | :--- |
| B | Branch |
| B,L | Branch and link |
| BLR | Branch and link register |
| BV | Branch vectored |
| BVE | Branch vectored external |
| BE | Branch external |
| B,E,L | Branch external and link |

When the L completer is used on an instruction, the instruction must specify which register is the link register—that is, which register is to get the return address. Typically, GR2 is used for calls within the space and GR31 for calls to another space. The reason GR2 is used for the B, L instruction is that there is a version of B, L that implicitly uses GR2 as the link register. By doing this, the 5 bits in the instruction that specify the link register can be used to specify the branch target. When using GR2 as the link register, the B, L instruction has a range of ±8 MB from the current instruction. Register GR2 is commonly called rp, for return pointer.

The BLR and BV instructions are used for branches to target addresses that are farther than 8 MB from the current instruction but still within the same space. BLR computes the target address by adding an offset to any of the general registers. This address is then used relative to the current instruction. This extends the range of the branch. The BV instruction is not relative to the current instruction—it uses two registers, a base register and a displacement register, to compute the target address. A common use of the BV instruction is to return from a procedure call. By using GR0 (which is always zero) as a displacement and rp as the base, we branch back to the return address saved by the B, L instruction that made the call. This instruction is sometimes seen as BV r0(rp) and sometimes just as RET.

The “external” versions of the branch instruction are essentially the same. The key differences are that they allow the specification of both space and offset as the target address, and they save both space and offset of the return address. They also store the offset of the return address into GR31 rather than GR2.

## Conditional Branch

There are four types of conditional branches in PA-RISC:

- Move and branch
- Compare and branch
- Add and branch
- Branch on bits

Each has two forms: one that compares two registers and another that compares a register and an immediate value. The immediate value is 5 bits, giving it a range of −16 to +15. The conditions for branching are specified as completers to the branch instruction. The mnemonics for these instructions are shown in Table 2-3.

### Table 2-3 Conditional Branch Instructions

| Instruction | Definition |
| :--- | :--- |
| MOV B | Move and branch |
| MOV I B | Move immediate and branch |
| CMP B | Compare and branch |
| CMP I B | Compare immediate and branch |
| ADD B | Add and branch |
| ADD I B | Add immediate and branch |
| BB | Branch on bit |

The MOV B and MOV I B instructions either copy a register to another register or copy an immediate value to a register. They then branch to the target address if the specified condition is true based on the value that was moved. Table 2-4 lists the possible conditions for the MOV and MOV I B instructions.

### Table 2-4 MOV B and MOV I B Instruction Conditions

| Condition | Definition |
| :--- | :--- |
| Never | |
| = | All bits in word are 0 |
| < | Leftmost bit in word is 1 |
| OD | Rightmost bit in word is 1 |
| TR | Always |
| ◇ | Some bits in word are 1 |
| >= | Leftmost bit of word is 0 |
| EV | Rightmost bit in word is 0 |

For example, the instruction MOV B, = r4, r5, main + 0x16 would move the contents of GR4 into GR5. If the value moved was zero, a branch would be taken to the address main + 0x16; otherwise, execution would continue in sequence.

The CMPB and CMPIB instructions either compare two registers or compare an immediate value and a register. The instruction then branches to the target address if the specified condition is true; otherwise execution continues in sequence. Table 2-5 shows the possible conditions for the CMP and CMPIB instructions.

### Table 2-5 Conditions for CMP and CMP IB Instructions

| Condition | Definition |
| :--- | :--- |
| Never | |
| = | Operand 1 is equal to operand 2 |
| < | Operand 1 is less than operand 2 (signed) |
| <= | Operand 1 is less than or equal to operand 2 (signed) |
| << | Operand 1 is less than operand 2 (unsigned) |
| <<= | Operand 1 is less than or equal to operand 2 (unsigned) |
| SV | Operand 1 minus operand 2 overflows (signed) |
| OD | Operand 1 minus operand 2 is odd |
| TR | Always |
| ◇ | Operand 1 is not equal to operand 2 |
| >= | Operand 1 is greater than or equal to operand 2 (signed) |
| > | Operand 1 is greater than operand 2 (signed) |
| >>= | Operand 1 is greater than or equal to operand 2 (unsigned) |
| >> | Operand 1 is greater than operand 2 (unsigned) |
| NSV | Operand 1 minus operand 2 does not overflow (signed) |
| EV | Operand 1 minus operand 2 is even |

For example, the instruction `CMPIB, <= . 7, r3, main+0x18` would compare the value in GR3 to the immediate value 7. If 7 <= GR3 (or, to put it another way, if, GR3 > 7), the instruction would branch to `main+0x18`.

The `ADDB` and `ADDIB` either add two registers or add an immediate value to a register. If the result satisfies the condition, then the branch is taken. Table 2-6 lists possible conditions for the `ADDB` and `ADDIB` instructions.

### Table 2-6 Conditions for ADD and ADD IB Instructions

| Condition | Definition |
| :--- | :--- |
| Never | |
| = | Operand 1 is equal to negative of operand 2 |
| < | Operand 1 is less than negative of operand 2 (signed) |
| <= | Operand 1 is less than or equal to negative of operand 2 (signed) |
| NUV | Operand 1 plus operand 2 does not overflow (unsigned) |
| ZNV | Operand 1 plus operand 2 is zero or no overflow (unsigned) |
| SV | Operand 1 plus operand 2 overflows (signed) |
| OD | Operand 1 plus operand 2 is odd |
| TR | Always |
| <> | Operand 1 is not equal to negative of operand 2 |
| >= | Operand 1 is greater than or equal to negative of operand 2 (signed) |
| > | Operand 1 is greater than negative of operand 2 (signed) |
| UV | Operand 1 plus operand 2 overflows (unsigned) |
| VNZ | Operand 1 plus operand 2 is nonzero and overflows (unsigned) |
| NSV | Operand 1 plus operand 2 does not overflow (signed) |
| EV | Operand 1 plus operand 2 is even |

As an example, consider the instruction ADDIB, OD 17,r4,main+0x18. The value 17 is added to the contents of GR4, and the result is placed in GR4. If the result is odd, then the branch to main+0x18 will be taken.

The branch on bit instruction examines a bit in a register and conditionally branches based on that bit. The arguments to the instruction are the register, the position of the bit, and the target address. Table 2-7 lists the possible conditions for the BB instruction. The position argument can be a fixed bit position, or it can be SAR, which refers to the Shift Amount Register (CR11).

### Table 2-7 Conditions for BB Instruction

| Condition | Definition |
| :--- | :--- |
| < | Leftmost bit in word is 1 |
| >= | Leftmost bit in word is 0 |

## Delayed Branching

All branching in PA-RISC uses a feature known as delayed branching. This means that the instruction immediately following the branch will be executed even if the branch is taken. This instruction following a branch is called the delay slot. Consider the following code:

```
LDW0x20(x30), r2
COMIB,>10,r2,main+80
LDw0x24(x30), r3
```

The first instruction loads the value from 0x20 past GR30 into GR2. Next, the compare instruction compares that value to 10 and branches to main+80 if GR2 < 10. The next LDW
