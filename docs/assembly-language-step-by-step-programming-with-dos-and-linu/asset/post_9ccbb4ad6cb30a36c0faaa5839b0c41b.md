
# Not the End, But Only the Beginning 529

This is a huge book (1,300+ pages) covering code optimization, largely for graphics applications (where it matters the most) but explained in a way that can be applied to almost anything. Some of involves C programming, but most of it is pure, expert-level assembly—and on the CD-ROM is the original text of Michael's 1989 classic Zen of Assembly Language, which was barely off when its publisher went under. The book was then lost in the crash of a big reorganization, and it never recovered. You'll need to get some practice and some context before all of this book will be completely comprehensible, but it's fully written and whether you can read it now, grab it if you see it so it'll be there on your shelf when you're ready for it. (Alas, it went out of print in early 2000, just as I am completing the book you're now reading.)

# Stepping off Square One

Okay—with a couple of new books in hand and good night's sleep behind you, strike out on your own a little. Set yourself a goal, and try to achieve it: something tough, say, an assembly language utility that locates all files anywhere on a hard disk drive with a given ambiguous file name. That's ambitious for a newcomer and will take some research and study and (perhaps) a few false starts. But you can do it, and once you do it'll be a real journeyman assembly language programmer.

Becoming a master takes work, and time. Michael Abrash's massive Graphics Programming Black Book (recently out of print but still in some stores) is a compilation of the secret knowledge of a programming master. It's not easy reading, but it will give you a good idea where your mind has to be to consider yourself an assembly language programmer.

Keep programming. Michael can show you things that would have taken years to discover on your own, but they won't stick in your mind unless you use them. Set yourself a real challenge, something that has to be both correct and fast: Rotate graphics objects in 3-D, transfer data through a serial port at 19,200 bits per second, things like that.

You can do it.

Coming to believe the truth in that statement is the essence of stepping away from Square One—and the rest of the road, like all roads, is taken one step at a time.

# APPENDIX A

# Partial 8086/8088 Instruction Set Reference

| Instruction | Reference Page | Text Page |
|---|---|--|
| AAA | 535 | 310 |
| ADC | 536 | 201 |
| ADD | 538 | 11 |
| AND | 540 | 67 |
| BT | 542 | 466 386+ |
| CALL | 543 | 454 |
| CLC | 544 | |
| CLD | 545 | 374 |
| CMP | 546 | 183 |
| DEC | 548 | 21 |
| IMUL | 549 | 309 |
| INC | 551 | 11 |
| INT | 552 | 86 |
| IRET | 553 | 263 |
| JZ | 554 | Only in Appendix A |
| JXZ | 556 | 389 |
| JECXZ | 557 | 422 |

| Instruction | Reference Page | Text Page |
|---|---|---|
| JMP | 558 | 190 |
| LEA | 559 | Only in Appendix A |
| LOOP | 560 | 276 |
| LOOPNZ/LOOPNE | 561 | 389 |
| LOOPZ/LOPE | 562 | 422 |
| MOV | 563 | 75 |
| NEG | 564 | 212 |
| NOP | 565 | Only in Appendix A |
| NOT | 566 | 213 |
| OR | 567 | 67 |
| POP | 568 | 214 |
| POPA | 569 | 253 286+ |
| POPAD | 569 | 253 386+ |
| POPF | 570 | 253 |
| POPFD | 571 | 465 386+ |
| PUSH | 572 | 115 |
| PUSHA | 573 | 251 286+ |
| PUSHAD | 574 | 251 386+ |
| PUSHF | 575 | 85 |
| PUSHFD | 576 | 465 386+ |
| RET | 577 | 263 |
| ROL | 578 | 316 |
| ROR | 580 | 316 |
| SBB | 582 | 11 |
| SHL | 583 | 316 |
| SHR | 585 | 316 |
| STC | 587 | Only in Appendix A |
| STD | 588 | 376 |
| STOS | 589 | 596 |
| SUB | 590 | 140 |
| XCHG | 592 | 198 |
| XOR | 593 | 86 |

# Notes on the Instruction Set

## Instruction Operands

When an instruction takes two operands, the destination operand is the one on the left, the source operand is the one on right. In general, when a result is produced by an instruction, it replaces the destination operand. For example, in this instruction:

ADD BX, SI the BX register is added to SI register, and the sum is then placed in the BX register, overwriting whatever was in BX before addition.

## Flag Results

Each instruction contains a flag summary that looks like this (the asterisks vary from instruction to instruction):

```
O D I S Z A P C Overflow flag TF: Trap flag AF: Aux carry
F F F F F F DF: Direction flag SF: Sign flag PF: Parity flag
* * * * * IF: Interrupt flag ZF: Zero flag CF: Carry flag
```

The nine flags are all represented here. An asterisk indicates that the instruction on page affects that flag. If a flag is affected at all (it has an asterisk beneath it), it will be affected by these rules:

- OF Set the result is too large to fit in the destination operand.
- IF Set by STI; cleared by CLI.
- TF For debuggers; not used in normal programming and may be ignored.
- SF Set when the sign of the result forces the destination operand to become negative.
- ZF Set if the result of an operation is zero. If the result is nonzero, ZF is cleared.
- AF Auxiliary carry used for 4-bit BCD math. When an operation causes a carry out of 4-bit quantity.
- PF Set if the number of 1 bits in the low byte of the result is even; cleared if the number of 1 bits of the result is odd. Used in data communications but little else.
- CF Set if the result of an add or shift operation carries out a bit beyond the destination operand; otherwise cleared. May be manually set by STC and manually cleared by CLC when CF must be in a known state before an operation begins.

Some instructions force certain flags to become undefined. When this is the case, it is noted under “Notes.” Undefined means don’t count on it being in any particular state.

# AAA Adjust AL after BCD Addition

Flags affected:

O D I S Z A P C OF: Overflow flag TF: Trap flag AF: Aux carry
F F F F F F DF: Direction flag SF: Sign flag PF: Parity flag
* IF: Interrupt flag ZF: Zero flag CF: Carry flag

Legal forms:

AAA

Examples:

AAA makes an addition come out right in AL when you’re adding BCD values rather than ordinary binary values. Note well that AAA does not perform the arithmetic itself, but is a postprocessor after ADD or ADC The AL register is an implied operand and may not be explicitly stated—so make sure that the preceding ADD or ADC instruction leaves its results in AL!

A BCD digit is a byte with the high 4 bits set to 0, and the low 4 bits containing a digit from 0 to 9. AAA will yield garbage results if the preceding ADD or ADC acted upon one or both operands with values greater than 09.

After the addition of two legal BCD values, AAA will adjust a non-BCD result (that is, a result greater than 09 in AL) to a value between 00 and OC, since it is the carry of a BCD digit and not simply the 0 and 9. This is called a decimal carry, since

For example, if added 08 and 04 (both legal BCD values) to produce 0C in AL, AAA will take the 0C and adjust it to 02. The decimal carry goes to AH, to the upper 4 bits of AL, which are always cleared to 0 by AAA.

If the preceding ADD or ADC resulted in a decimal carry (as in the preceding example), both CF and AF are set to 1 and AH is incremented by 1. Otherwise, AH is not incremented and CF and AF are cleared to 0.

This instruction is see the detailed discussion in Chapter.

```
r8 = AH AL BH CH CL DH  r16 = AX CX DX SP SI DI
sr = CS DS SS FS            r32 = EAX EBX ECX ESI
m8 = 8-bit memory data   m16 = 16-bit memory data
m32 = 32-bit memory data      i8 = 8-bit immediate data
i16 = 16-bit immediate data  i32 = 32-bit immediate data
d8 = 8-bit signed displacement d16 = 16-bit signed displacement
d32 = 32-bit unsigned displacement
```

# ADC Arithmetic Addition with Carry

Flags affected:

O D I S Z A P C OF: Overflow flag TF: Trap flag AF: Aux carry
F F F F F F DF: Direction flag SF: Sign flag PF: Parity flag
* * * * * * IF: Interrupt flag ZF: Zero flag CF: Carry flag

Legal forms:

```
ADC r8,r8
ADC m8,r8
ADC r8,m16
ADC r16,r16
ADC m16,r16
ADC r16,m16
ADC r32,r32 386+
ADC m32,r32 386+
ADC r32,m32 386+
ADC r8,i8
ADC m8,i8
ADC r16,i16
ADC m16,i16
ADC r32,i32 386+
ADC m32,i32 386+
ADC r16,i8
ADC m16,i8
ADC r32,i8 386+
ADC m32,i8 386+
ADC AL,18
ADC AX,i16
ADC EAX,i32 386+
```

Examples:

```
ADC BX, DI
ADC EAX, 5
ADC AX, 0FFFFH ;Uses single-byte opcode
ADC AL, 42H ;Uses single-byte opcode
ADC BP, 17H
ADC WORD [BX+SI+Inset],5
ADC WORD ES:[BX],0B800H
```

# Notes:

ADC adds the source operand and the Carry flag to the destination operand, and after the operation, result replaces the destination operand. The add operation is an arithmetic add, and the carry allows multiple-precision additions across several registers or memory locations.( To add without taking the Carry flag into account, use the ADD instruction.)
