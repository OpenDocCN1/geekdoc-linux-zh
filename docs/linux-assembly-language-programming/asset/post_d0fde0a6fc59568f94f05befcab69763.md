
*   *imm* stands for *immediate*. The term *immediate* is used to refer to a numerical value given directly by a decimal or hexadecimal representation as opposed to a register or memory location containing that value.

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

But `MOV AL, -129` is not valid in Edlinas because -129 is not in the eight-bit signed range. NASM doesn't balk until it gets to -257. NASM allows characters to represent ASCII codes. For example,

### Table 3.13. x86 General Registers

| 8-bit | 16-bit | 32-bit |
| :---- | :----- | :----- |
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

### 3.11.2 MOV reg,reg

MOV reg,reg copies from the second register into the first. The two-operand commands described in this book use the syntax COMMAND destination, source. Hence the command

```
MOV EAX, EBX
```

does not change the EBX register. It means

let EAX = EBX

*not* move EAX to EBX.

There are assemblers which use the opposite syntax, such as the AT&T-style assembler used by gcc. In its syntax, the exact same command is written

```
movl %ebx, %eax
```

The two registers used in a `MOV` command must be the same size. The following command, for example, is not valid.

```
MOV EBX, DX
```

### 3.11.3 Ambiguity Problem

According to the append H hex convention discussed in *chapter 2, section 2.7*, the register names `AH`, `BH`, `CH`, and `DH` are also valid hexadecimal names for the numbers ten, eleven, twelve, and thirteen. This would make commands such as

```
MOV BL, AH
```

ambiguous. This command would be a valid example of both the **reg,reg** form and the **reg,imm** form of the `MOV` command. The customary resolution of this ambiguity is to require all hexadecimal numbers used in assembly language commands to begin with one of the digits 0, 1, . . . 9. This modification of the append H convention will be observed in this text and is required by both `NASM` and `Edlinas`. Hence `MOV BL, AH` is actually not a valid example of the **reg,imm** form. It is an example of the **reg,reg** form. To store the immediate value ten into `BL` we must use either

```
MOV BL, 0AH

or

MOV BL, 10
```

## 3.12 Addition and Subtraction Commands

This section describes the **reg,imm** and **reg,reg** forms of the `ADD` and `SUB` commands. These are very fundamental arithmetic instructions.

### 3.12.1 ADD reg,imm

```
ADD reg,imm
```

means to add the immediate value to the register. For example

```
ADD BL, 10
```

can be thought of as

```
let BL = BL + 10
```

### 3.12.2 ADD reg,reg

The command

```
ADD reg, reg
```

means to add the contents of the second register to the first. So the command

```
ADD BL, AL
```

means

```
let BL = BL + AL
```

The register AL is not changed by this command.

### 3.12.3 SUB reg,imm

The command

```
SUB BL, 10
```

for example, means

```
let BL = BL -10
```

### 3.12.4 SUB reg,reg

```
SUB BL, AL
```

for example, means

```
let BL = BL - AL
```

## 3.13 Multiplication and Division Commands

If the multiplication command were to function similarly to the ADD and SUB command, we would expect to see commands such as

```
MUL EAX, EBX
```

which would mean to multiply the contents of the register EAX by the value in EBX. However, the multiply command does not work like this. One reason is that because multiplying numbers together typically doubles them in size, it does not make sense to use the same size registers for the answer as for the multiplied numbers.

### 3.13.1 The MUL Command

The syntax for the multiply command is

```
MUL reg
```

reg may be any of the 24 general registers listed in Table 3.13. If the register used is an eight-bit register, for example

```
MUL BH
```

then the command means:

let AX = AL • BH

When an eight-bit register is used, it always multiplies by AL and stores the result in AX. When a 16-bit register is used, for example,

```
MUL BX
```

then the command means

let DX:AX = AX • BX

where the 32-bit answer is stored in two 16-bit registers. The top 16 bits are stored in DX, the bottom 16 bits in AX. When a 32-bit register is used, for example,

```
MUL EBX
```

then the command means

let EDX:EAX = EAX • EBX

A single register is all that you specify when you use the MUL command. The other registers are always implied. The situation is similar to that with the ADD command on the 8080 processor, where addition results are always stored in the A register. The command ADD B in 8080 assembly language means

let A = A + B

Unlike the ADD and SUB commands, the MUL command has no immediate form. The command

```
MUL 7
```

is not valid.

### 3.13.2 The DIV Command

The DIV command closely resembles the MUL command in syntax and is essentially its inverse. It forms both a quotient and a remainder

| Form | dividend | remainder | quotient |
| :--- | :------- | :-------- | :------- |
| 32-bit | EDX:EAX | EDX | EAX |
| 16-bit | DX:AX | DX | AX |
| 8-bit | AX | AH | AL |

For example, if AX held the value 17 and BH held the value 3, then

```
DIV BH
```

would store 2 in AH and 5 in AL. The command would be recognized as an eight-bit command because BH is an eight-bit register.

Division by zero produces an error called an exception. Exceptions are dealt with in chapter 9.

It is important to note that because of the sizes of the registers involved in division, zero is not the only divisor which can cause an exception. For example, when AX is divided by a number stored in an eight-bit register, the quotient is supposed to be stored in AL, an eight-bit register. But dividing a 16-bit number by an eight-bit number does not always produce a number which can be stored in eight bits. For example, 1024 ÷ 2 = 512, or in hex, 400H÷2 = 200H. But 200H requires at least ten bits of storage. This means that the

following code will cause an exception:

```
MOV AX, 400H
MOV BH, 2
DIV BH
```

This error is called a *division overflow*.

### 3.13.3 Negative Numbers and Congruences

Two's complement representation is used for negative numbers, in part because it allows addition and subtraction hardware to be used irrespective of whether the bits being operated on are intended as signed integers or as unsigned integers. The mathematical explanation for why two's complement representation works like this is based on a concept due to C. F. Gauss, a remarkable nineteenth century mathematician.

Gauss defined $a \equiv b$ (mod m) to mean that $a$ and $b$ differ only by some exact multiple of m. In two's complement representation, a negative number and the positive number used to represent it differ by the turnover value of the registers being used. If four-bit registers are being used, then each negative and its positive representation differ by $2^4$, or 16, as shown in Table 3.9. In Gauss' notation, for example, $-5 \equiv 11$ (mod 16). So when the computer does $(-2) + (-3)$ as $14 + 13$, it depends on the fact that $14 + 13 = 27 \equiv -5$ (mod 16). The four-bit addition hardware produces 11 because a carry of 16 is lost. But that is okay. Eleven is the correct representative for -5.

**Congruence Addition Theorem**

This reasoning is summarized in the following theorem due to Gauss:

> $$\begin{aligned} &\text{If } a \equiv b \text{ (mod m) and } c \equiv d \text{ (mod m)} \\ &\text{then } a + c \equiv b + d \text{ (mod m)} \end{aligned}$$

This theorem says that congruences can be added just like equations. Gauss devised the congruence notation in order to make the point that a congruence is similar to an equation.

**Congruence Multiplication Theorem**

The following theorem states that congruences can also be multiplied just like equations.

> $$\begin{aligned} &\text{If } a \equiv b \text{ (mod m) and } c \equiv d \text{ (mod m)} \\ &\text{then } a \cdot c \equiv b \cdot d \text{(mod m)} \end{aligned}$$

Because of this nice theorem, we should be able to use both signed and unsigned numbers with MUL just like ADD and have no problems! Except for one thing.

We want to double the register size as we go. So the theorem we really need is this one:

> $$\begin{aligned} &\text{If } a \equiv b \text{ (mod m) and } c \equiv d \text{ (mod m)} \\ &\text{then } a \cdot c \equiv b \cdot d \text{ (mod } \text{m}^{2}\text{)} \end{aligned}$$

Unfortunately, this isn't a theorem. It's a falsehood. For example, in the eight-bit case where $\text{m} = 256$ and $\text{m}^{2} = 65,536$, if $a = -16$, $b = 240$, and $c = d = 2$, we get $a \cdot c = -32$ and $b \cdot d = 480$. So the theorem says $$-32 \equiv 480 \text{ (mod } 256\text{)}, \text{which is correct.}$$ Removing the eight-bit turnover value of 256 from 480 leaves 224. Hence if we considered the answer to be
