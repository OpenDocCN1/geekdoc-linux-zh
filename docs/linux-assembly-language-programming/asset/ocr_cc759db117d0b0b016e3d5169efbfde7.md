letters are upper case.

+   4. If the first byte is OF, then a whole raft of possibilities is opened up. The information conveyed by OF is merely "go to Table 5.4."

# Table 5.2. First Byte of Opcode Space

| | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | A | B | C | D | E | F |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 0 | ADD<br>rm,ib | ADD<br>rm,ib | ADD<br>rm,ib | ADD<br>AL,ib | ADD<br>AL,ib | ADD<br>AX,iw | PUSH<br>ES | OR<br>ES | OR<br>rm,v,iw | OR<br>rm,v,iw | OR<br>AL,ib | OR<br>eAX,ib | OR<br>eAX,il | PUSH<br>DS | 386<br>space | |
| 1 | ADC<br>rm,ib | ADC<br>rm,ib | ADC<br>rm,ib | ADC<br>AL,ib | ADC<br>AL,ib | ADC<br>AX,iw | PUSH<br>SS | SBB<br>rm,v,iw | SBB<br>rm,v,iw | SBB<br>AL,ib | SBB<br>AX,iw | SUB<br>rm,v,iw | SUB<br>rm,v,iw | SUB<br>AL,ib | SUB<br>eAX,il | POP<br>DS | DS |
| 2 | AND<br>rm,ib | AND<br>rm,ib | AND<br>rm,ib | AND<br>AL,ib | AND<br>AL,ib | AND<br>AX,iw | DA<br>ES: | SUB<br>rm,v,iw | SUB<br>rm,v,iw | SUB<br>AL,ib | SUB<br>AX,iw | XOR<br>rm,v,iw | XOR<br>rm,v,iw | XOR<br>AL,ib | XOR<br>AX,iw | DAS |
| 3 | XOR<br>rm,v,iw | XOR<br>rm,v,iw | XOR<br>AL,ib | XOR<br>AX,iw | AAA | CMP<br>rm,v,iw | CMP<br>rm,v,iw | CMP<br>AL,ib | CMP<br>AX,iw | CMP<br>rm,v,iw | CMP<br>rm,v,iw | CMP<br>AL,ib | CMP<br>AX,iw | CMPSB<br>CS: | AAS |
| 4 | INC<br>rm,v,iw | INC<br>rm,v,iw | INC<br>AL | INC<br>AX | DEC<br>rm,v,iw | DEC<br>rm,v,iw | DEC<br>AL | DEC<br>AX | DEC<br>rm,v,iw | DEC<br>rm,v,iw | DEC<br>AL | DEC<br>AX | DEC<br>rm,v,iw | DEC<br>rm,v,iw | DEC<br>AL | DEC<br>AX | |
| 5 | PUSH<br>ES | PUSH<br>CS | PUSH<br>SS | PUSH<br>DS | PUSH<br>eAX | POP<br>ES | POP<br>CS | POP<br>SS | POP<br>DS | POP<br>eAX | POP<br>ES | POP<br>CS | POP<br>SS | POP<br>DS | POP<br>eAX | |
| 6 | POPA | POPA | POPD | POPD | CALL<br>fs: | OPLen<br>AdLen | PUSH<br>ES | PUSH<br>CS | PUSH<br>SS | PUSH<br>DS | PUSH<br>eAX | PUSH<br>ES | PUSH<br>CS | PUSH<br>SS | PUSH<br>DS | PUSH<br>eAX | |
| 7 | Jb<br>ib | Jb<br>ib | Jb<br>ib | JA<br>ib | JAE<br>ib | JB<br>ib | JBE<br>ib | JS<br>ib | JNS<br>ib | JP<br>ib | JNP<br>ib | JE<br>ib | JNE<br>ib | JG<br>ib | JGE<br>ib | JGL<br>ib | JLE<br>ib | JNL<br>ib | JG<br>ib |
| 8 | Imssd<br>rm,ib | Imssd<br>rm,ib | Imssd<br>rm,ib | Imssd<br>rm,ib | Imssd<br>rm,ib | TEST<br>rm,ib | TEST<br>rm,ib | XCHG<br>AX,iw | XCHG<br>CX,iw | MOV<br>rm,ib | MOV<br>rm,ib | MOV<br>rm,ib | CALL<br>rv,m | LOOP<br>LEA<br>rv,m | LOOP<br>mov<br>rx,m | LOOP<br>mov<br>rw,m | |
| 9 | NOP | XCHG<br>AL,iv | XCHG<br>AX,iv | XCHG<br>CL,iv | XCHG<br>CX,iv | XCHG<br>DL,iv | XCHG<br>DX,iv | XCHG<br>BSWAP<br>ECW<br>CQD | CWQ<br>CWD<br>FWAIT | PUSHF<br>POP<br>SAHF | PUSHF<br>POP<br>SAHF | |
| A | MOV<br>AL,iv | MOV<br>AX,iv | MOV<br>CL,iv | MOV<br>CX,iv | MOV<br>DL,iv | MOV<br>DX,iv | MOV<br>STOSB<br>AL,iv | STOSW<br>AL,iv | LODSB<br>LDOSW<br>LODSB | LODSW<br>SCASB<br>SCASW | SCASW |
| B | MOV<br>AL,ib | MOV<br>CL,ib | MOV<br>DL,ib | MOV<br>BL,ib | MOV<br>AH,ib | MOV<br>CH,ib | MOV<br>DH,ib | MOV<br>BH,ib | MOV<br>ECX,il | MOV<br>EDX,il | MOV<br>ESP,il | MOV<br>EBP,il | MOV<br>ESI,il | MOV<br>EDI,il | |
| C | Shift<br>rm,v,iw<br>1 | Shift<br>rm,v,iw<br>2 | Shift<br>RET<br>rm,iv | RET<br>rm,iv | INT 22 | INT<br>iv | ENTER<br>iw,iw | RETF<br>iw | RETF<br>iv | IRET<br>INTO<br>IRET | |
| D | Shift<br>rm,v,iw<br>1 | Shift<br>rm,v,iw<br>2 | AAM<br>rm,ib | AAD<br>rm,ib | XLATB | 87 | 87 | 87 | 87 | 87 | 87 | 87 | 87 | |
| E | LOOPNS<br>short<br>REPE | LOOP
NS<br>short<br>REPE | LOOP<br>short<br>REPE | JCCZ<br>short<br>REPE | CALL<br>in<br>out<br>eax,ilb | OUT<br>eax,ilb<br>Unasy<br>rmv | CALL<br>out<br>eip,ilb | JMP<br>in<br>AX | JMP<br>out<br>AX | IN<br>eax,ilb<br>AL,OUT<br>AX,ilb | OUT<br>eax,ilb<br>IN,OUT<br>IncDec<br>rm,ib | In/De<br>rv,mv |
| F | LOCK | REPE<br>HLT | CMC<br>Unasy<br>rmv | CLC<br>Unasy<br>rmv | STC<br>Unasy<br>rmv | CLI<br>Unasy<br>rmv | STI<br>Unasy<br>rmv | CLD<br>Unasy<br>rmv | STD<br>Unasy<br>rmv | |

+   5. If the first byte is in the range D8-DF, then the command is a floating point command. These commands are not dealt with in this text.

+   6. There are also prefix bytes which modify the subsequent commands. In Table 5.2, the prefix bytes such as the **LOCK** prefix F0 are shown as *bottom-sitters*.

These various cases are dealt with one by one in the following sections.

# 5.3 The ModRM Byte

The ModRM byte is used to carry operand information when the first byte cannot do so. The ModRM byte consists of three parts.

| Mod | R | M |
|---|---|---|
| 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |

+   1. Bits 7 and 6 are the Mod bits. When the Mod bits are 11, the M bits designate a register. Otherwise the M bits are used for memory coding.
+   2. Bits 5, 4, and 3 are the R, or register, bits and are often designated using a slash notation, */r*.
+   3. Bits 2, 1, and 0 are the M, or memory, bits, and are used to specify or help specify a memory location except when the Mod bits are 11.

# 5.3.1 rv,rmv Coding

The entry in Table 5.2 for the byte 03 is