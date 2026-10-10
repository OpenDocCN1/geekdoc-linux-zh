
; Use EDX to store a decrement counter for the y = y + x loop.
;
        MOV EDI, 100H ; Initialize pointer into y.
        MOV ESI, 200H ; Initialize pointer into x.
;
; y = y + x
        MOV EDX, 40H    ; Loop needs 64 iterations.
        CLC             ; Clear the carry flag.
XYZ:     MOV EAX, [ESI]  ; 4 Source bytes into the Processor.
        ADC [EDI], EAX    ; Do the addition.
        INC ESI
        INC ESI           ;
        INC ESI           ; This is ugly.
        INC ESI
        INC EDI           ; But using ADD here would
        INC EDI           ; clear the carry flag.
        INC EDI
        INC EDI
        DEC EDX           ; Decrement the loop counter.
        JNZ XYZ           ; See if the loop is finished.

lines which would have resulted from using the [imm] format.

At first sight it would appear that we could do better by using ADD instructions in place of multiple INC instructions. But this would actually ruin everything. Because we are using a loop to proceed four bytes at a time from the least significant to the most significant bytes, we encounter a problem with the carry flag. If in between two executions of the ADC instruction we move four bytes down the number using an ADD instruction, we have messed up the carry flag. In chapter 4 it is noted that the carry flag is unaffected by the INC and DEC instructions. The reason for this arcane little exception suddenly becomes clear. Multibyte arithmetic needs a carry flag which can survive loop counter adjustments. Because they don't affect the carry flag, the INC and DEC instructions can be used to carry out harmless loop counter adjustments. Adding 4 by using four INC instructions is not beautiful, but it works.

This code is not bad from the standpoint of taking up memory space since memory is cheap. But it is bad from the standpoint of adding execution time to a loop. If there is one place where execution time is costly it is in the middle of a nested loop, and that is exactly where those extra INC instructions are.

Another memory format is useful in dealing with this problem.

## 6.2.3 The [reg+scale*reg+imm] Format

The most general memory format is the [reg + scale * reg + imm] format, where scale is a scale factor which must be either 1, 2, 4, or 8. The register which is multiplied by the scale factor is called the index register. The other register is called the base register. Some fields may be omitted. This gives us the effect of a variety of formats, including

-   [scale*reg + imm]
-   [reg + scale*reg]
-   [reg + reg + imm]
-   [reg + imm]
-   [reg + reg]

in addition to the [reg] and [imm] formats already discussed. It is a little hard to believe that instructions with this degree of complexity are hardcoded into the processors. But the cost in terms of instruction length for all this complexity is actually just one more byte of code for instructions which utilize this general format. The byte is called the SIB byte, both for scaled-index-base byte and sibling of the ModR/M byte.

Taking up the problem of the repeated INC instruction in Program 6.3, note that a scale factor of 4 would increase the address by **4** whenever the index register was incremented by **1**. In the code shown in Program 6.5 the `[scale*reg + imm]` format is used to refer to both source and destination memory locations. In this code we see that a single `INC` instruction takes the place of eight `INC` instructions in Program 6.3.

### Program 6.5

```assembly
;
;	Edlinas program which finds 256-byte powers of 3.
;	Store the 256 bytes of x starting at memory address 100H.
;	Store the 256 bytes of y starting at memory address 200H.
		MOV EBX, 3 ; Initialize base.
		MOV EDX, 1 ; Initialize exponent.
;	y = 3
		MOV EAX, 0 ; Do the adding in EAX.
		MOV EDI, 40H ; Loop needs 64 iterations.
ZRO:		DEC EDI
		MOV [4*EDI + 200H], EAX
		JNZ ZRO
		MOV [4*EDI + 200H], EBX
;
;	x = y. Main infinite loop starts here.
;	
LUP:		MOV EDI, 40H ; Loop needs 64 iterations.
		MOV ESI, EBX ; Initialize main loop counter.
BEG:		DEC ESI
		MOV EAX, [4*EDI + 200H]
		MOV [4*EDI + 100H], EAX
		JNZ BEG
;	y = y + x
AGN:		MOV ECX, 40H ; Loop needs 64 iterations.
XYZ:		MOV EAX, [4*EDI + 200H]
		ADC EAX, [4*EDI + 100H]
		MOV [4*EDI + 200H], EAX
		INC EDI
		DEC ECX
		JNZ XYZ
;		DEC ESI
		JNZ AGN
;		INC EDX
		JMP LUP
```

One variation which is not permitted is the use of memory references in both operand positions. There are no x86 processor instructions which use memory as both source and destination operands. The instruction

```assembly
ADD [EAX], [EBX]
```

for example, does not exist. There however are instructions which involve both reading from and writing to memory; `INC [EAX]`, for example both reads from and writes to the memory location whose address is in EAX. Architectures called *load/store* architectures do not allow mixing processor operations with memory operations. The only commands in a load/store architecture which access memory are *load* and *store*.

## 6.2.4 16-Bit Addresses

In section 6.2.2 the `[reg]` format for memory addressing was presented where `reg` could be any of the eight 32-bit general registers. The 8086 and 80286 also use a `[reg]` format. Not all eight 16-bit registers are permitted; however, only `BP`, `BX`, `SI`, and `DI`. There is also a `[reg + reg + imm]` form. `imm` must be a 16-bit number. If two registers are used, the only allowed combinations are, `BP + SI`, `BP + DI`, `BX + SI`, and `BX + DI`. Since these restrictions are easy to forget, programmers not accustomed to 16-bit addresses may find themselves using disallowed forms of address. Most programmers will prefer to avoid 16-bit addressing whenever possible.

These 16-bit forms of memory address can be used on an 80386. When they occur in 32-bit code, a special prefix, 67H, has to be applied to the machine code to notify the processor that the memory address bits in the ModR/M byte are coded using the old 16-bit coding system. This prefix is called the address size prefix. It is similar to the operand size prefix discussed in chapter 5, section 5.5.

## 6.2.5 CISC vs. RISC

An x86 computer is generally considered to be a complex instruction set computer (CISC). This is partly because of complicated addressing, as in the [EDX + 4*ESI + ABC] memory operand. Machines such as the SUN and MIPS workstations are based on the idea that by simplifying the instructions and having fewer of them, they become easier and faster to execute. This can more than make up for the fact that it takes more of these little instructions to write a program. Computing based on this philosophy is called RISC, reduced instruction set computing. The RISC vs. CISC issue is not an either-or issue like little endian vs. big endian. RISC is a set of features which may be adopted partially, in varying degrees. One reason that the 486 and Pentium processors were able to compete with the early RISC PowerPC processors is that they adopted a partial RISC philosophy. Although CISC instructions are allowed on a Pentium, it works faster if programmed using a RISC-like subset of the total instruction set.

Their names notwithstanding, the Pentium II and Pentium Pro have gone over to a totally RISC architecture. The instruction set used internally is a pure RISC instruction set. Traditional x86 instructions are converted internally to RISC instructions before they are executed. In a sense, the "end of the line" tag hung on the Pentium by Apple marketers was correct. But ironically, 386 assembly language is now stronger than ever.

## 6.3 Operand Size Ambiguity

In most two-operand instructions, both operands must have the same size. So when a memory operand is used in such a context, the number of bytes it refers to can be determined if the other operand is a register operand. For example, in ADD [EBX], AX the memory operand [EBX] must refer to two bytes of memory since AX is a two-byte register. However, when a memory operand is used with an immediate operand, the result is ambiguous. For example, the following command is ambiguous:

```assembly
MOV [EBX], 5
```

Similarly, when a memory operand is used with a unary operation such as NEG (which takes the two's complement of a number), the operand size is indeterminate. An instruction such as

```assembly
NEG [EBX]
```

might well refer to one, two, or four bytes of memory. Under these circumstances, an assembler has to make a choice. NASM chooses to produce an error message. In 32-bit code Edlinas defaults to a four-byte reference when the reference is ambiguous. In 16-bit code, the default is two-byte. To indicate the one-byte case in Edlinas you may use the customary but clumsy notation

```assembly
NEG BYTE PTR [EBX]
```

In NASM, the code is

```assembly
NEG BYTE [EBX]
```

To indicate a four-byte reference in NASM, the code is

```assembly
NEG DWORD [EBX]
```

A two-byte reference is indicated using WORD as a qualifier. These qualifiers clearly do the job. The implied concession that a word is 16 bits is unfortunate. In light of notation such as BYTE PTR, the AT&T practice of adding a letter to the mnemonic doesn't seem so bad. In fact, the Intel assembler does use mnemonics of this sort in a few cases such as LODSB and STOSB (load string byte and store string byte).

## 6.4 Labels
