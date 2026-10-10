
# 4.4 Assembler Programs with Jumps

High-level languages need loops in order to be able to do their work. These loops must be turned into assembly code by a compiler. For example, as illustrated in Figure 4-2, to do a C language while loop in the most straightforward way requires both a conditional jump forward and an unconditional jump backward.

![](img/a3d6758e6e21b80b35e1b981ecbc1234_62_0.png)

![](img/a3d6758e6e21b80b35e1b981ecbc1234_63_0.png)

## 4.4.1 The JMP Command

The fetch-execute cycle works by calculating the address in memory of the next instruction. This address is normally determined by just going to the first address beyond the current instruction. In order to support if-then statements or loops in high-level languages, however, jumps are needed. The *JMP* command transfers execution to the address specified by a label.

The *JMP* command has the form:

```
JMP label
```

The label is created by the programmer. It is wise to devise labels which help in understanding the program. For this purpose, long labels are useful. On the other hand, the screen space used by Edlinas is very limited and so labels beyond three characters are truncated when they are displayed unless they are on a line by themselves. The label in the label field specifies the target of the jump and often has a colon appended to make it clear that it is a label and not an arcane mnemonic. Many jump commands may point to the same target, but no two lines may carry the same label in their label field. In the following program, the last line transfers control to the preceding line. This program continues adding 2 to the *EAX* register forever. It is an infinite loop. Infinite loops are usually written only by mistake.

## 4.4.2 Conditional Jumps and Flags

A *conditional jump* is a jump carried out on the basis of a truth value. The information on which such decisions are based is contained in one-bit registers called *flags*. When a flag contains 1, it is referred to as being *set*. When it contains 0, it is referred to as being *cleared*. Two very important flags are the zero flag and the sign flag.

### Program 4.3

```
        MOV EAX, 0
        MOV EBX, 2
XYZ:    ADD EAX, EBX
        JMP XYZ
```

## The Zero and Sign Flags

The *ADD* and *SUB* commands affect not only their destination registers but also many of the flags. Suppose the command:

```
ADD EAX, EBX
```

is executed. The result of this command will be in the EAX register. If this result is 0, then the zero flag is set. If it is not 0, then the zero flag is cleared.

The value given to the sign flag after an *ADD* instruction is the value of the most significant bit of the result. This bit is 1 if the result is negative when viewed as a signed number. Thus if executing the *ADD EAX, EBX* command gives *EAX* a value which is negative, as a four-byte signed number, then the sign flag is set; otherwise the sign flag is cleared.

## 4.4.3 The JZ, JS, JNZ, and JNS Commands

The following conditional jump commands all have the same format as the JMP command.

| Command | Label |
| :--- | :--- |
| JZ | label |
| JS | label |
| JNZ | label |
| JNS | label |

They each take a label in the operand field. The meanings of these commands are as follows:

| Command | Meaning |
| :--- | :--- |
| JZ | Jump if the zero flag is set. |
| JS | Jump if the sign flag is set. |
| JNZ | Jump if the zero flag is not set. |
| JNS | Jump if the sign flag is not set. |

The following assembly language program illustrates the use of the *JS* instruction in a program to determine which of two user inputs is larger. Program 4.4 seems air tight. In fact it has a bug.

### Program 4.4

```
; If the first input is larger output 1
; If the second input is larger output 2
; The program uses subtraction:
; B < A is true if and only if B - A is negative.
; A subtraction followed by a JS does the job
;
	MOV EDX, 0
	IN EAX, [DX] ; The first input is now in EBX
	MOV EBX, EAX
	IN EAX, [DX] ; The second input is now in EAX.
	SUB EBX, EAX ; This is (first - second).
	JS SIB ; Second is Bigger
	MOV EAX, 1 ; Otherwise First is Bigger
	JMP END ; Don't drift into the other case!
SIB:	MOV EAX, 2 ;
END:	MOV EDX, 1 ; Either way now EAX is ready.
	OUT [DX], EAX
	RET
```

# 4.5 Assembler Programs with Loops

Conditional jumps are used to implement loops and if-then statements. Suppose we consider the following program, which does multiplication using repeated addition. For example to do 7 × 5 we can do 5 + 5 + 5 + 5 + 5 + 5 + 5. In Program 4.5 the number 1 is added in one line and subtracted in another. There are special commands for this which take less memory space.

### Program 4.5

```
;
	MOV EDX, 0
	IN EAX, [DX] ; First input is the multiplier
	MOV EBX, EAX ; Put Multiplier in EBX
	IN EAX, [DX] ; Second input is the multiplied number
	MOV ECX, 0 ; Initialize the running total.
RPT:	ADD ECX, EAX ; Do one addition.
	SUB EBX, 1 ; One less yet to be done.
	JNZ RPT ; If that's not zero, do another.
	MOV EAX, ECX ; Put the total in EAX
	ADD EDX, 1 ;
	OUT [DX], EAX ; Output the answer.
```

# The INC and DEC Commands

The following increment and decrement commands add and subtract 1:

```
INC reg
```

and

```
DEC reg
```

*reg* may be any of the 24 general registers. These commands are often used to increment or decrement a loop counter. In Program 4.5, `SUB EBX, 1` can be replaced by `DEC EBX` and `ADD EDX, 1` can be replaced by `INC EDX`.

# 4.6 Signed Comparisons

## 4.6.1 Comparison-Based Jumps

High-level languages often use comparisons in if-then statements. Using the sign flag to test the result of a subtraction, as was done in section 4.4, seems to be a reasonable way to implement this testing since it is a mathematical fact that:

```
B < A if and only if B - A is negative.
```

Since the sign flag indicates the sign of the result of a subtraction we would seem to be on solid ground. But in fact this is not true.

## 4.6.2 The Overflow Flag

Suppose we are using one-byte signed numbers and we wish to test whether:

```
100 < -50
```

In one-byte registers:

```
100 - (-50) = -106
```

An overflow has occurred. The result is negative. The sign flag is set and the comparison will be judged as true! Using the sign flag to determine a jump gives the wrong answer. But since an overflow always changes the sign of a result to the opposite of what it should be, the jump condition can be fixed.

- 1. If no overflow has occurred, jump if the sign flag is set.
- 2. If an overflow has occurred, jump if the sign flag is not set.

The x86 processor has an overflow flag. It is used in order to implement this fixed-up jump condition. If we use SF for the binary value of the sign flag and OF for that of the overflow flag, we can restate the fixed jump condition as just:

```
Jump if (SF XOR OF)
```

This jump condition will produce a jump following a subtraction such as:

```
SUB AL, BL
```

if and only if `AL < BL`. There is an x86 command for this jump. The mnemonic for it is *JL*, which stands for *jump if less than*.

## 4.6.3 The CMP Command

When a subtraction is performed only for the sake of a comparison, it may be done with the *CMP* instruction. This command sets the flags in the exact same way as *SUB* but has the advantage of not wasting register space by storing an unneeded result. Using the *JL* and *CMP* instructions we can rewrite the Program 4.4 as follows:

### Program 4.6

```
; If the first input is larger output 1
; If the second input is larger output 2
; The program uses subtraction:
; B < A is true if and only if B - A is negative.
MOV EDX, 0
IN EAX, [DX]
MOV EBX, EAX    ;The first input is now in EBX
IN EAX, [DX]    ;The second input is now in EAX.
CMP EBX, EAX    ; This is first - second.
JL SIB          ; Second is Bigger
MOV EAX, 1      ; Otherwise First is Bigger
JMP END         ; Don't drift into the other case!
SIB:
MOV EAX, 2
END:
MOV EDX, 1      ; Either way now EAX is ready.
OUT [DX], EAX
RET
```

Program 4.6 works correctly for all numbers in the unsigned four-byte range.

## 4.6.4 More Jump Commands

Following a *CMP EAX, EBX* command, the *JL* command executes a jump if the condition `EAX < EBX` is true. The commands:

```
CMP EAX, EBX
JL ABC
```

mean:

- Compare *EAX* to *EBX*
- Jump if *EAX* is less than *EBX*

What is going on here is subtraction and flag checking, but the well-designed syntax allows us to overlook that. The *less than* condition is not the only condition conveniently accessed following a *CMP* command. A list of several other conditional jump commands is given here.

| Command | Condition | Example |
| :--- | :--- | :--- |
| JL | less than | EAX < EBX |
| JLE | less than or equal | EAX <= EBX |
| JG | greater than | EAX > EBX |
| JGE | greater than or equal | EAX >= EBX |
| JE | equal | EAX = EBX |
| JNL | not less than | EAX ? EBX |
| JNLE | not less than or equal | EAX ? EBX |
| JNG | not greater than | EAX ? EBX |
| JNGE | not greater than or equal | EAX ? EBX |
| JNE | not equal | EAX ? EBX |
