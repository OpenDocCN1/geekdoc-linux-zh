
The following code will cause an exception:

```asm
MOV AX, 400H
MOV BH, 2
DIV BH
```

This error is called a *division overflow*.

### 3.13.3 Negative Numbers and Congruences

Two’s complement representation is used for negative numbers, in part because it allows addition and subtraction hardware to be used irrespective of whether the bits being operated on are intended as signed integers or as unsigned integers. The mathematical explanation for why two’s complement representation works like this is based on a concept due to C. F. Gauss, a remarkable nineteenth century mathematician.

Gauss defined $a \equiv b \ (\text{mod } m)$ to mean that $a$ and $b$ differ only by some exact multiple of $m$. In two’s complement representation, a negative number and the positive number used to represent it differ by the turnover value of the registers being used. If four-bit registers are being used, then each negative and its positive representation differ by $2^4$, or 16, as shown in Table 3.9. In Gauss' notation, for example, -5 $\equiv$ 11 (mod 16). So when the computer does $(-2) + (-3)$ as $14 + 13$, it depends on the fact that $14 + 13 = 27 \equiv -5$ (mod 16). The four-bit addition hardware produces 11 because a carry of 16 is lost. But that is okay. Eleven is the correct representative for -5.

**Congruence Addition Theorem**

This reasoning is summarized in the following theorem due to Gauss:

If $a \equiv b \ (\text{mod } m)$ and $c \equiv d \ (\text{mod } m)$
then $a + c \equiv b + d \ (\text{mod } m)$

This theorem says that congruences can be added just like equations. Gauss devised the congruence notation in order to make the point that a congruence is similar to an equation.

**Congruence Multiplication Theorem**

The following theorem states that congruences can also be multiplied just like equations.

If $a \equiv b \ (\text{mod } m)$ and $c \equiv d \ (\text{mod } m)$
then $a \cdot c \equiv b \cdot d \ (\text{mod } m)$

Because of this nice theorem, we should be able to use both signed and unsigned numbers with MUL just like ADD and have no problems! Except for one thing.

We want to double the register size as we go. So the theorem we really need is this one:

If $a \equiv b \ (\text{mod } m)$ and $c \equiv d \ (\text{mod } m)$
then $a \cdot c \equiv b \cdot d \ (\text{mod } m^2)$

Unfortunately, this isn't a theorem. It’s a falsehood. For example, in the eight-bit case where $m = 256$ and $m^2 = 65,536$, if $a = -16$, $b = 240$, and $c = d = 2$, we get $a \cdot c = -32$ and $b \cdot d = 480$. So the theorem says 224 unsigned or -32 signed, then everything would be okay. Two hundred twenty-four is the two's complement positive that is equivalent to -32 in the eight-bit system. But we're not content with eight bits. We want 16. And $-32 \equiv 480 \ (\text{mod } 65,536)$ is wrong.

In the 16-bit system, -32 is represented by 65504, not 480. Consequently, we can't use MUL (or DIV) for both signed and unsigned numbers. MUL and DIV work for unsigned numbers. There are different commands which work for signed numbers: IMUL and IDIV. This is an example of the issue raised in section 3.6.5.

## Further Reading

- *The Microprocessor, A Biography*, Michael S. Malone, Springer: 1995.
- *The Anatomy of a High-Performance Microprocessor*, Shrber and Smith, IEEE: 1998.

## Chapter 4. ASSEMBLY LANGUAGE

A computer program is something which can be stored in a computer's memory. If the memory has one-byte words, we can then say that the computer program consists of bytes. These bytes are also called *machine language*. Writing a program by listing these bytes explicitly is called *machine language programming*. It is the original form of programming. It is definitely the most tedious. Assembly language was devised as a way of specifying machine code without actually having to write it down. Assembly language may be mere shorthand or it may involve complex *macros*, some of which may even resemble *if or while* statements in C. But whether it is primitive or fancy, its defining characteristic is that it gives the programmer control over the machine language.

Three good reasons for learning assembly language are:

1. In truly time-critical sections of code, it is sometimes possible to improve performance by coding in assembly language.
2. It is a good way to learn how a particular CPU works.
3. In writing a new operating system or in porting an existing system to a new machine, there are sections of code which must be written in assembly language.

Assembly languages are written to fit hand-in-glove with a specific processor. Given the considerable variety of processors and instruction sets, one might expect there to be a considerable variety in the instruction formats for the various assembly languages as well. But this is not the case. Assembly languages generally follow one universal format which might be called the *four field format*.

### 4.1 The Four Field Format

According to this format every assembly language program consists of lines. Every line consists of four fields. The four fields are the label field, the mnemonic field, the operand field, and the comment field.

1. The label field is used for a label which specifies the target of a jump instruction. A jump is the same as a *go to* instruction. Examples of jump instructions are given in *section 4.4*.
2. The mnemonic field contains an instruction specifier. Examples of mnemonics are *MOV*, *ADD*, *SUB*, *etc*. The word *mnemonic* suggests that it makes the machine code easy to remember, although it doesn't; it makes the machine code unnecessary to remember.
3. The operand field contains the object or objects on which the instruction is operating. If there is more than one operand, they are separated by commas. As we noticed above, *ADD* takes two operands. *JMP* on the other hand takes one. Some mnemonics take none at all.
4. The comment field contains documentation. It begins with a semicolon. In any computer language, documentation is important. In assembly language, documentation is especially important because an assembly language program is especially hard to read without it. A line may consist of nothing but a comment.

Program 4.1 is an example of an x86 assembly language program. The reader should note the consistent four field layout even though some of the fields on some of the lines are empty. Many of the instructions in Program 4.1 are making their first appearance here in this book. These new instructions are all discussed in this chapter.

#### Program 4.1

```asm
;
; Greatest common divisor program
;
MOV  EDX, 0      ; 0 is the only Edlinas input port
IN   EAX, [DX]   ; Get the user’s first input
MOV  ECX, EAX    ; Get the input out of harm’s way
IN   EAX, [DX]   ; Get the user’s second input
MOV  EDX, EAX    ; Use EDX for the larger of the two inputs
ORD:
   SUB  EAX, ECX  ; Use EAX as a working copy of EDX
   JZ   GCD       ; When equality is obtained we are done.
   JNS  NXT       ; We want EDX to be larger. No swap needed
   MOV  EAX, ECX  ; Swap EDX and ECX (Takes three MOV’s)
   MOV  ECX, EDX
NXT:
   MOV  EDX, EAX  ; If there was no swap then EDX = EDX-ECX
   JMP  ORD       ; End of the loop
GCD:
   MOV  EAX, EDX  ; The GCD is in EDX
   MOV  EDX, 1    ; We need EDX for the output port number
   OUT  [DX], EAX ; Display the answer to the user
   RET
```

### 4.2 Computers from the CPU Standpoint

Computers are often described as consisting of three parts: the CPU, the memory, and the input/output, or I/O system. A diagram drawn according to this picture looks like Figure 4-1. Included in the I/O system are the monitor, the keyboard, the hard drive, the printer, the modem, the sound card, and the CDROM. These are all just I/O devices. This is a processor-centric view. Just as members of a group sometimes categorize people in terms of how they relate to the group, this picture of a computer defines parts of a computer according to how they relate to the CPU. Since assembly language is all about working with the CPU, however, it is a useful point of view for us to adopt.

Figure 4-1. All Computers are Divided into Three Parts

![](img/a3d6758e6e21b80b35e1b981ecbc1234_58_0.png)

If we imagine the CPU in the picture to be a 386, then we can think of the data bus as a set of 32 wires connected to 32 pins on the CPU, and the address bus as another set of 32 wires also connected to the CPU. Notice that the memory and I/O systems are connected to the processor in essentially the same way. If we
