letters are upper case.

4. If the first byte is 0F, then a whole raft of possibilities is opened up. The information conveyed by 0F is merely "go to Table 5.4."

# Table 5.2. First Byte of Opcode Space

| | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | A | B | C | D | E | F |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 0 | ADD | ADD | ADD | ADD | ADD | PUSH | OR | OR | OR | OR | OR | OR | OR | PUSH | 386 | space |
| | r/m8,v | r/m8,v | r/m8,v | AL,LB | AL,LB | r/m16 | | 88,v | r/m,v | r/m,v | r/m,v | AL,IB | eAX,II | CS | |
| 1 | ADC | ADC | ADC | ADC | ADC | PUSH | SUB | SBB | SBB | SBB | SBB | SBB | SBB | POP | DS |
| | r/m,v | r/m,v | r/m,v | AL,IB | AL,IB | eAX,II | r/m,v | r/m,v | r/m,v | r/m,v | r/m,v | AL,IB | eAX,II | | |
| 2 | AND | AND | AND | AND | AND | AND | DAA | SBB | SUB | SUB | SUB | SUB | SUB | SUB | DAS | CS: |
| | r/m,v | r/m,v | r/m,v | r/m,v | AL,IB | eAX,II | | 9,IB | r/m,v | r/m,v | r/m,v | AL,IB | eAX,II | | |
| 3 | XOR | XOR | XOR | XOR | XOR | XOR | AAA | CMP | CMP | CMP | CMP | CMP | CMP | CMP | AAS |
| | r/m,v | r/m,v | r/m,v | r/m,v | AL,IB | eAX,II | | r/m,v | r/m,v | r/m,v | r/m,v | r/m,v | r/m,v | r/m,v | |
| 4 | INC | INC | INC | INC | INC | INC | DEC | DEC | DEC | DEC | DEC | DEC | DEC | DEC | ADI |
| | eAX | eCX | eDX | eBX | eSP | eBP | eSI | eDI | eAX | eCX | eDX | eBX | eSP | eBP | |
| 5 | PUSH | PUSH | PUSH | PUSH | PUSH | PUSH | PUSH | POP | POP | POP | POP | POP | POP | POP | POP |
| | r/m,16 | eAX | eCX | eDX | eBX | eSP | eBP | eSI | eDI | eAX | eCX | eDX | eBX | eSP | eSI |
| 6 | PUSHA | POPA | POPD | ARPL | | | PUSH | MUL | PSHL | INSIL | INSIB | INSID | OUTSB | OUTSD | |
| | | m,m2 | m,m2,2 | FS: | GS: | QP,Len | Ad,Len | | | | | | | | |
| 7 | JO | JNO | JB | JAE | JE | JNE | JBE | JA | JS | JNS | JP | JNP | JL | JGE | JG |
| | IB | IB | IB | IB | IB | IB | IB | IB | IB | IB | IB | IB | IB | IB | IB |
| 8 | Imovsd | Imovsd | Imovsd | TEST | TEST | XCHG | XCHG | MOV | MOV | MOV | MOV | MOV | LEA | MOV | MOV |
| | r/m,v | r/m,v | r/m,v | r/m8,IB | r/m,v | r/m,v | r/m,v | r/m,v | r/m,v | r/m,v | m,v | m,n | r/m,v | r/m,v | r/m,v |
| 9 | NOP | XCHG | XCHG | XCHG | XCHG | XCHG | XCHG | XCHG | XCHG | CWD | CWO | CALL | FWAIP | PUSHF | SAHF | LAHF |
| | | eAX, | eCX, | eDX, | eBX, | eSP, | eBP, | eSI, | eDI, | | | r/m,IB | CALL | POPF | | |
| | | eAX, | eAX, | [v,L,A] | [v,L,A] | [v,L,A] | [v,L,A] | [v,L,A] | [v,L,A] | | | | | | |
| A | MOV | MOV | MOV | MOV | MOVSB | MOVSW | CMPSB | CMPSW | TEST | TEST | STOIB | LOOBD | LOOBS | SCASB | SCASW |
| | AL,[v] | eAX, | eAX, | [v,L,A] | [v,L,A] | [v,L,A] | AL,IB | eAX,IV | AL,IB | eAX,IV | AL,IB | | | AL, | |
| B | MOV | MOV | MOV | MOV | MOV | MOV | MOV | MOV | MOV | MOV | MOV | MOV | MOV | MOV | MOV |
| | AL,IB | CL,IB | DL,IB | BL,IB | AH,IB | CH,IB | DH,IB | BH,IB | r/m,IB | r/m,IB | eCX,IV | eDX,IV | r/m,IV | eSP,IV | eSI,IV |
| C | Shift | Shift | Shift | RET | IESP | INT | ENTER | RETF | RETF | RETF | RETF | RETF | IN | INTO | IRET |
| | r/m,IV | r/m,IV | r/m,IV | | 12 | INT,IB | 12 | | IV,12 | IV,12 | IV,IB | IV,IB | IV,IB | | |
| D | Shift | Shift | Shift | AAM | AAD | | XLEATB | 87 | 87 | 87 | 87 | 87 | 87 | 87 | 87 |
| | r/m,IV | r/m,IV | r/m,IV | | | | r/m, | space | space | space | space | space | space | space | space |
| E | LOOPI | LOOPF | LOOP | JOCC | OUT | OUT | CALL | JMP | JMP | JMP | CALL | INT | IN | OUT | |
| | short | LOOP | short | | r/m,1B | eAX,II | [v,L,A] | [v,L,A] | IV, | IV, | ALL,IB | ALL, | OAX,IB | OAX,IB | INC/Dec |
| F | LOCK | | REP | REPZ | CMC | Uray | Uray | CLC | STC | CLI | STI | CLD | STD | | Indr |
| | | | REPE | REPE | | r/m,v | r/m,v | | | | | | | | | m,v |

5. If the first byte is in the range D8-DF, then the command is a floating point command. These commands are not dealt with in this text.

6. There are also prefix bytes which modify the subsequent commands. In Table 5.2, the prefix bytes such as the **LOCK** prefix F0 are shown as *bottom-sitters*.

These various cases are dealt with one by one in the following sections.

# 5.3 The ModRM Byte

The ModRM byte is used to carry operand information when the first byte cannot do so. The ModRM byte consists of three parts.

| | Mod | R | M |
|---|---|---|---|
| | 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |

+   1. Bits 7 and 6 are the Mod bits. When the Mod bits are 11, the M bits designate a register. Otherwise the M bits are used for memory coding.

+   2. Bits 5, 4, and 3 are the R, or register, bits and are often designated using a slash notation, *r*/*r*.

+   3. Bits 2, 1, and 0 are the M, or memory, bits, and are used to specify or help specify a memory location except when the Mod bits are 11.

# 5.3.1 r/v,r/mv Coding

The entry in Table 5.2 for the byte 03 is