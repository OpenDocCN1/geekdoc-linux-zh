# Unconditional Branch

Table 2-2 shows the types of unconditional branches. The external branches are used to branch to a location in a different space: the vectored branches branch to an address held in a register; and the link branches save the return address in a register.

# Table 2-2 Unconditional Branches

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

# Conditional Branch

There are four types of conditional branches in PA-RISC: