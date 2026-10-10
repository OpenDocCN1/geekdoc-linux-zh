
## 5.3.1 ADD EDI, EAX

We can use this entry to assemble the ADD EDI, EAX command. The ADD EDI, EAX command requires a ModRM byte. The `m` in the second operand position specifies not only that the second operand may be a memory operand, but also that it must be encoded in the M bits of the ModRM byte. Since the second operand is the register EAX, the bit code for EAX, 000, occupies the M bits in the ModRM byte. Since we are using a register for the M bits, the two Mod bits must be 11. The first operand, which as the `r` indicates must be a register, is therefore encoded in the R bits of the ModRM byte. EDI is the first operand and its code is 111. Consequently the ModRM byte is:

| Mod | R | M |
|---|---|---|
| 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |
| 1 | 1 | 1 | 1 | 1 | 0 | 0 | 0 |

$1111\ 1000 = \text{F8H}$

Combining the 03 with the ModRM byte yields the code `03 F8` for `ADD EDI, EAX`.

If in this code we change the two Mod bits from 11 to 00, we get the code for `ADD EDI, [EAX]`. Here the M bits are used for an actual memory operand. The codes 01 and 10 are used to code for immediate displacements such as `ADD EDI, [EAX + 5]`, where the displacement is either of type `ib` or `iv`. Hence the code for `ADD EDI, [EAX + 5]` is `03 78 05`. The code for `ADD EDI, [EAX + 87654321H]` is `03 B8 21 43 65 87`. If this coding were done uniformly, however, it would leave no room in the coding space for the complicated formats seen in chapter 6, section 6.2.3. To make space for coding these formats, the code for the ESP register is removed to provide an escape into another byte of the coding space called the SIB byte.

## 5.3.2 rmv, rv Coding

When the `rmv` and `rv` keys are reversed, this turns the three-bit codes around. As an example, suppose we want to code the instruction `MOV EDI, EAX`. The entry for `8B` matches and could be coded with the same ModRM byte as the `ADD EDI, EAX` code. But the entry `89` also matches:

```
MOV
rmv, rv
```

Using this entry, we note that the first operand may be a register and is coded in the M bits. Hence the code for EDI goes into the least significant bits. The second operand, EAX, is coded in the R bits.

| Mod | R | M |
|---|---|---|
| 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |
| 1 | 1 | 0 | 0 | 0 | 1 | 1 | 1 |

$1100\ 0111 = \text{C7H}$

Hence, using the 89 entry in Table 5.2, we obtain the encoding `89 C7` for `MOV EDI, EAX`.

## 5.3.3 Nonregister R Bits

In some cases, the first byte is insufficient to specify an operation, but the R bits of a ModRM byte are used to complete the specification. These cases are listed in Table 5.3. `SUB ECX, 32` is an example. The entry in Table 5.2 for `83` is:

```
Immed
rmv, ib
```

Since the row of Table 5.3 labeled "Immed" has a SUB under `ir = /5`, we learn that instructions matching:

```
SUB
rmv, ib
```

can be coded using `83` as the first byte and `101` for the R bits of the ModRM byte. Since the first operand, ECX, is not memory, the Mod bits must be 11, and the M bits will be filled with `001`, the code for ECX. So the required ModRM byte is:

### Table 5.3. Instructions Specified by R Bits

|  /r | /0 000 | /1 001 | /2 010 | /3 011 | /4 100 | /5 101 | /6 110 | /7 111 |
|---|---|---|---|---|---|---|---|---|
| Immed | ADD | OR | ADC | SBB | AND | SUB | XOR | CMP |
| Shift | ROL | ROR | RCL | RCR | SHL | SHR | SAR | |
| Unary | TEST i | NOT | NEG | MUL | IMUL | DIV | IDIV | |
| IncDec | INC | DEC | DEC | | | | | |
| Indir | INC | DEC | CALL m | CALL FAR m | JMP | JMP FAR | PUSH | |

| Mod | R | M |
|---|---|---|
| 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |
| 1 | 1 | 1 | 0 | 1 | 0 | 0 | 1 |

$1110\ 1001 = \text{E9H}$

The `ib` stands for an immediate byte. So the code for `SUB ECX, 32` is `83 E9 20`.

## 5.4 386 Space (OF + ...)

On an 8086, the byte `OF` codes for the instruction `POP CS`. On subsequent processors this instruction was removed to make the `OF` code available for a significant expansion in the instruction set. Table 5.4 reveals the space which was opened up. Like Table 5.2, it shows the information conveyed by a single byte, in this case the byte following an initial `OF` byte. A few of the instructions in Table 5.4 appeared first on the 80286, the 80486, or the Pentium, but most of them appeared first on the 80386. The bulk of the instructions new to the 80286 are in Table 5.2.

- As with Table 5.2, sometimes one entry specifies exactly one instruction. For example, `OF CA` is the code for the instruction `BSWAP EDX` (Byte SWAP the EDX register).
- Sometimes a ModRM byte is needed to convey operand information. The XADD instruction whose first two bytes are `OF C1` is an example of this.
- Sometimes a ModRM byte is used to specify an operation. For example, if the first two bytes of the instruction are `OF 01`, then we must check R bits of the ModRM byte to determine the operation. From Table 5.5 we see that if the register bits in the ModRM byte were `011` then the instruction would be an LIDT instruction (Load the Interrupt Descriptor Table).

### Table 5.4. 386 Space

| | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | A | B | C | D | E | F |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 0 | LOCKIT | GRANTIT | LAR PU,IBY | LSL PU,IBY | | | UDM,AL | CLTS | | | INVD | WNSWD | | | | | |
| 1 | | | | | | | | | | | | | | | | |
| 2 | MOV r2,DRi | MOV r2,CRi | MOV CRi,2 | MOV DRi,2 | MOV r2,DRi | | MOV TRi,2 | | | | | | | | | | |
| 3 | WRMSR | RDTSR | RDMSR | | | | | | | | | | | | | |
| 4 | | | | | | | | | | | | | | | | |
| 5 | | | | | | | | | | | | | | | | |
| 6 | MMX space | MMX space | MMX space | MMX space | MMX space | MMX space | MMX space | MMX space | MMX space | MMX space | MMX space | MMX space | MMX space | MMX space | MMX space | MMX space |
| 7 | MMX space | MMX space | MMX space | MMX space | MMX space | MMX space | MMX space | MMX space | MMX space | MMX space | MMX space | MMX space | MMX space | MMX space | MMX space | MMX space |
| 8 | JO | JNO | JB | JAE | JE | JNE | JBE | JA | JS | INS | JP | JNP | JL | JGE | JLE | JG |
|   | iv | iv | iv | iv | iv | iv | iv | iv | iv | iv | iv | iv | iv | iv | iv | iv |
| 9 | SETO | SETNO | SETB | SETAE | SETE | SETNE | SETBE | SETA | SETS | SETNS | SETP | SETNP | SETL | SETGE | SETLE | SETG |
|   | m8 | m8 | m8 | m8 | m8 | m8 | m8 | m8 | m8 | m8 | m8 | m8 | m8 | m8 | m8 | m8 |
| A | PUSH | POP | CPUID | BT | SHLD | SHLD | BUL | PUSH | POP | RSM | BTS | SHRD | SHRD | BSR | MOVX | IMUL |
|   | FS | FS | FS | cv, rm | cv, rm | cv, rm | r, m16 | m16, gs | r | m8 | rmv r, m8 | rmv r, ib | rmv r, m8 | rm | rmv r, m8 | r, rm |
| B | CMPOVP | LSS | LFS | LOGS | MOVX | MOVX | CMOVS | BSWAP | BSWAP | BSWAP | BSWAP | BSWAP | BSWAP | BSWAP | BSWAP | BSWAP |
|   | mv, m8 | m8 | m8 | m8 | r, rm | r, rm | m8 | m8 | m8 | m8 | m8 | m8 | m8 | m8 | m8 | m8 |
| C | XADD | XADD | MXC | | MXC | | | | | | | | | | | |
| D | | | | | | | | | | | | | | | | |
| E | | | | | | | | | | | | | | | | |
| F | | | | | | | | | | | | | | | | |

Some of the codes refer to MMX instructions. These instructions are discussed in the Intel book, *The Complete Guide to MMX Technology*.

We learn that instructions matching Table 5.5 contain 80486, Pentium, and MMX instructions as well as 80386 instructions. For example, the XADD and BSWAP instructions first appeared on the 80486 and the CPUID and RDTS C first appeared on the Pentium.

### Table 5.5. OF Instructions Specified by R Bits

| /r | /0 000 | /1 001 | /2 010 | /3 011 | /4 100 | /5 101 | /6 110 | /7 111 |
|---|---|---|---|---|---|---|---|---|
| LocalT | SLD rm2 | STR rm2 | LLDT rm2 | LTR rm2 | VERR rm2 | VERW rm2 | | |
| GlobalT | SGDT m6 | SIDT m6 | LGDT m6 | LIDT m6 | SWGS rm2 | | LMSR rm2 | |

## 5.5 32-Bit vs. 16-Bit Code

To this point we have discussed machine codes for commands involving 32-bit general registers only. We are now ready to consider the coding of the 16-bit general registers.

The `MOV ECX, EAX` command, as noted in section 5.1, can be encoded as `89 C1`. The corresponding 16-bit command is `MOV CX, AX`. Surprisingly, the code for this command is also `89 C1`! The 80386 was designed to use the same encodings for the 16-bit registers as for the 32-bit registers. Clearly there is a problem with this. When the processor fetches the bytes `89 C1`, which instruction should be executed, `MOV ECX, EAX` or `MOV CX, AX`? It so happens that the decision is based on a single bit in the processor. This bit determines whether code is interpreted as 32-bit code, in which case `89 C1` means `MOV ECX, EAX`, or 16-bit code, in which case `89 C1` means `MOV CX, AX`.

When the bit is set it does not mean that the instruction `MOV CX, AX` is unavailable. To encode the fact that the 32-bit coding presumption is wrong a one-byte prefix `66` is used. So in 32-bit code `66 89 C1` is the code for `MOV CX, AX`. Similarly the `MOV ECX, EAX` instruction is available in 16-bit code. The code for it is `66 89 C1`. This prefix is called the operand size prefix. It means that the operand size is not the default size.

Typically the bit is set while running Linux for example, and cleared while running DOS. Except where specifically stated otherwise, code given in this book assumes the processor’s bit is set for the 32-bit default. Hence, `89 C1` means `MOV ECX, EAX` and `66 89 C1` means `MOV CX, AX`. Now that we see how the code `89 C1` can have either one of two possible meanings, it is easy to explain the

### Table 5.6. 32- vs. 16-Bit Coding Example

| | 32-Bit Code | 16-Bit Code |
|---|---|---|
| MOV ECX, EAX | 89 C1 | 66 89 C1 |
| MOV CX, AX | 66 89 C1 | 89 C1 |
