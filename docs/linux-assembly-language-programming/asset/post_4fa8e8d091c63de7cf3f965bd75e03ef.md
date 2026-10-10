
This is okay.

On the other hand the command may be coming from software that is using unsigned numbers. In this case the software sees the arithmetic that has just happened as

$$255 + 255 = 254.$$

This is not okay. The true answer, 510, has gone out of the one-byte unsigned range, 0-255. Hence the addition of FFH to FFH clears the overflow flag because the signed arithmetic answer is okay and sets the carry flag to notify software that there is an unsigned, out of range error.

As another example, suppose that one-byte registers receive a command to add 40H to 40H. The sum is 80H. If the above and below are used in place of the phrases greater than and less than. Hence the "jump if the arithmetic just done will appear as

$$64 + 64 = 128.$$

This is okay.

Suppose that the command has come from software working with signed numbers. Then the arithmetic looks like this:

$$64 + 64 = -128.$$

This is not okay. The true answer, +128, is outside the one-byte signed range, -128 to +127. The hardware sets the overflow flag because this is an out of range error in the signed number system, and clears the carry flag because there is no out of range error in the unsigned system. The hardware does not know which system the software is using, so it has to take care of both flags.

Both the carry and the overflow flags are out of range indicator flags. The carry flag is set if the arithmetic interpreted in the unsigned system has produced an out of range error. The overflow flag is set if the arithmetic interpreted in the signed system has produced an out of range error.

### 4.7.3 Still More Jump Commands

Given that we need a different command for "jump if less than" for use with unsigned numbers, we also need a different mnemonic. Moreover, considering all the other jump conditions, "greater than," "greater than or equal to," etc., we need a whole new set of commands and mnemonics. To systematize this new set, the words above and below are used in place of the phrases greater than and less than. Hence the "jump if less than" command which works for unsigned numbers uses the mnemonic $J_{B}$, for "jump if below." The full set of these commands is as follows:

- JBE below or equal EAX = EBX
- JA above EAX > EBX
- JAE above or equal EAX >= EBX
- JNB not below EAX = EBX
- JNBE not below or equal EAX ? EBX
- JNA not above EAX ? EBX
- JNAE not above or equal EAX ? EBX

## 4.8 Linux .s files

One of the intermediate steps that gcc uses in the translation of a C source program into an a.out file is an assembly language file. This file is the output of the compiler proper and the input to the assembler, gas. To see these assembler files, one can direct gcc to output the assembler file once this stage is reached using the -S switch. This output has a .s file extension. Consider for example the following C program, mult.c:

**Program 4.7**

```C
main()
{
	int x, y;
	register int a, b, c;
	printf("Enter a number: ");
	scanf("%d", &x);
	printf("Multiply it by what number?");
	scanf("%d", &y);

	a = x;
	b = y;
	c = 0;

	while (b != 0)
	{
		c = c + a;
		b = b - 1;
	}

	printf("The result is %d.\n", c);
}
```

Suppose that the numbers x = 5 and y = -7 are entered. This program actually outputs the correct answer, -35, and to calculate it, the loop executes $2^{32}$ - 7 = 4,294,967,289 times. Note that

$$(2^{32} - 7) \times 5 = 2^{32} \times 5 - 7 \times 5$$

Each time the running total, b, exceeds the turnover value of $2^{32}$, $2^{32}$ is dropped from the total. This happens four times. The resulting value of b is $2^{32}$ - 35, which is the two's complement representation of -35.

One of the main practical uses of assembly language programming is in the coding of loops that execute so many times that an improvement in the time required for each execution actually makes a noticeable difference in the total run time. In a test on a 120 MHz Pentium, the 5 $\times$ -7 calculation required 110.90 seconds. To obtain the assembly code for this program, one can use the command

```
linuxbox$ gcc -S mult.c
```

The resulting file, mult.s, is the assembly code which was used by gcc to produce the executable file. The syntax of this assembly code differs from that of the widely used Intel assembly language used in this book, but it can still be deciphered. Comments for this purpose are added. The first line uses TEST. It is an instruction

**Program 4.8**

```
.L2:
	testl %esi,%esi	; Is ESI = 0
	jne	.L4		; If not go to L4
	jmp	.L3		; otherwise go to L3
.L4:
	addl %ebx,%edi	; Let EDI = EDI + EBX
	decl %esi		; Let ESI = ESI - 1
	jmp	.L2		; Go to L2
.L3:
```

similar to CMP, which will be discussed in the next chapter, %esi refers to the ESI register. Like CMP, the TEST command sets the zero flag if ESI = 0. The 1 at the end of many of these commands is used to specify the length of the operand, "long" in this case, and that means four bytes. Notice that the add uses a "COMMAND source destination" operand order, the opposite of that used in this book.

The loop consists of the six instructions shown. If we note that we can take some jumps out of the loop by testing whether ESI is zero at the end of the loop, we can reduce the loop from six instructions to three. The only change made was

**Program 4.9**

```
.L2:
    testl %esi,%esi
    jne .L4
    jmp .L3
.L4:
    addl %ebx,%edi
    decl %esi
    jne .L4 ; If ESI isn't 0 go to L4
.L3:
```

to the jump at the end of the loop. The modified file was compiled using using gcc.

```
linuxbox$ gcc mult.s
```

The resulting program was run and the computation of $5 \times -7$ took 76.14 seconds on the same machine.

### 4.8.1 The Pentium's Dual Pipeline

If we look at the time for each instruction to execute, in the first case we get

![](img/165a4f637c5eaccb372f5a82ca458a05_70_0.png)

This arithmetic assumes that the program spent all of its time in the loop. Comparing this with the length of one clock cycle,

![](img/165a4f637c5eaccb372f5a82ca458a05_70_1.png)

we find the amazing result that the time for two instructions to execute, 8.606 nanoseconds, is just a little over one clock cycle. Since one instruction per clock cycle is ideal under ordinary circumstances, what we have here is something special. It is an illustration of the Pentium's dual pipeline. When possible, the Pentium pairs instructions off and executes two at once. This is how rates of more than one instruction per clock cycle can be achieved. (There is actually another pipeline for floating point numbers.) The instruction pairing also explains why the 2:1 improvement we might have expected when we reduced the number of instructions in the loop from six to three did not materialize. What happened apparently was that the number of instruction pairs went from three to two, one of the two "pairs" being half-empty. The time 76.14 nanoseconds is .687 of 110.9 nanoseconds. This is approximately two-thirds, suggesting the use of two instruction pairs instead of three for each pass through the loop.

## Chapter 5. MACHINE LANGUAGE

Machine language is the language seen by the processor. The bytes fetched in the fetch-execute cycle are bytes of machine code. Assembly language can be defined as language which gives the programmer control over the machine code. Assembly language specifies machine code. This characteristic feature of assembly language will not be apparent without some familiarity with machine language. In this chapter the main features of x86 machine code are presented.

The process of converting assembly code into machine code is called *assembling*. A program which takes assembly language as input and produces machine language as output is called an *assembler*. It is similar to a compiler but it operates at a lower level.

Conversely, the process of turning machine code into assembly language is called *unassembling*. A program which does this is called an *unassembler*.

### 5.1 Assembling Simple Programs

To tell the whole story of the machine code for the x86 processors involves a lot of tricky detail. However, it is quite easy to specify machine code for the subset of the x86 assembly language used in all the numbered programs used in sections 4.3 through 4.5. Coding for this portion of x86 assembly language is given in Table 5.1. Most of the machine code is given in hex, but some of the bytes have to be given in binary. The number of bytes varies from one to six. The first line of the table, for example, shows that the code for *MOV* reg,reg is a two-byte code, the first of which is given in hex and the second in binary. The bytes given in binary are those which incorporate register codes. S S S in the binary coding represents the three-bit code for the *source* register. D D D represents the three-bit code for the *destination* register. The register codes are given at the bottom. Each "imm" occurring in a command specifies four additional bytes, which must be supplied by the programmer. Examples follow. Using Table 5.1, Program 5.1 can be machine assembled as follows:

**Table 5.1. Some 32-Bit Machine Coding**

| | First Byte | Second Byte | 4 More |
|---|---|---|---|
| MOV | reg,reg | 89 | 11 S S D D D | |
| MOV | reg, imm | 1 0 1 1 D D D | | |
| ADD | reg,reg | 01 | 1 1 S S D D D | |
| ADD | reg, imm | 81 | 1 1 0 0 D D D [1] | |
| SUB | reg,reg | 29 | 1 1 S S D D D | |
| SUB | reg, imm | 81 | 1 1 1 0 1 D D D [1] | |
| INC | reg | 0 1 0 0 D D D | | |
| DEC | reg | 0 1 0 0 1 D D D | | |
| IN | EAX, [DX] | ED | | |
| OUT | [DX], EAX | EF | | |
| RET | | C3 | | |
| INP | imm | E9 | 84 | |
| JZ | imm | 0F | 84 | |
| JNZ | imm | 0F | 85 | |
| JS | imm | 0F | 88 | |
| JNS | imm | 0F | 89 | |

[1] If reg is EAX, there is a shorter machine code.

#### 5.1.1 Register Codes

The first byte of the first command, BA, is encoded using the 1011 1DDD code given for *MOV* reg,imm. The DDD bits are filled in with the register code 010 for DX, which results in a binary code of 1011 1010 or a hex code of BA.

The second *MOV* command, *MOV* ECX, EAX is encoded as 89 C1 using the first line of the chart which specifies the second byte as 11 SSS DDD. EAX is the source register and its code is 000. ECX is the destination register and its code is 001. The resulting second byte is 11 000 001, which is C1.

**Program 5.1**

Label Source Code Address Machine Code
