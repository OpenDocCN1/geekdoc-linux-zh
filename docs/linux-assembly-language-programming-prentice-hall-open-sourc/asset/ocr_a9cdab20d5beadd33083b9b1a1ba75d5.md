+   - *imm* stands for *immediate*. The term *immediate* is used to refer to a numerical value given directly by a decimal or hexadecimal representation as opposed to a register or memory location containing that value.

For example, in

```
MOV AX, 54
```

the number 54 occurs as an immediate value. This command stores the number, 54, into the 16-bit register AX. This register is the same as the bottom 16 bits of the register EAX. The top 16 bits are unmodified. Since 54 = 36H, the command is the same as the command

```
MOV AX, 36H
```

The value assigned to the location must fit. The command

```
MOV AL, 999
```

is not valid because 999 will not fit into an eight-bit register. NASM and Edlinas allow signed integers. Hence

```
MOV AL, -128
```

is valid and does the same thing as

```
MOV AL, 128
```

But is not valid in Edlinas because -129 is not in the eight-bit signed range. NASM doesn't balk until it gets to -257. NASM allows characters to represent ASCII codes. For example,

# Table 3.13. x86 General Registers

| 8-bit | 16-bit | 32-bit |
|---|---|---|
| AH | AX | EAX |
| AL | BX | EBX |
| BH | CX | ECX |
| BL | DX | EDX |
| CH | BP | EBP |
| CL | SP | ESP |
| DH | SI | ESI |
| DL | DI | EDI |

```
MOV AL, -129
MOV AL, 'A'
```

stores the ASCII code for the letter A, which is 65, in AL.

Code using 32-bit registers will not run on x86 processors prior to the 80386. Although it is a characteristic of so-called "32-bit code" to use 32-bit registers, some "16-bit code" does also. The actual difference between 32- and 16-bit code is discussed in chapter 5, section 5.5.

# 3.11.2 MOV reg,reg

MOV reg,reg copies from the second register into the first. The two-operand commands described in this book use the syntax COMMAND destination, source. Hence the command