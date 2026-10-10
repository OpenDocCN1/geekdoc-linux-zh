
## 6.5 Assembler Directives
instructions to the assembler, it is better to call them assembler directives. Assembler directives typically lack the universality of processor instructions which usually follow the format laid down by the manufacturer. Edlinas follows the Unix tradition that all assembler directives begin with a dot, and uses .db.

Without the initial dot, the define byte syntax is very widespread. When used with labels it works in both Microsoft and Turbo assemblers. In these assemblers the define byte directive has the flavor of a data type declaration. This "data type" is used to resolve ambiguities of the kind noted in section 6.2. For example, if the label ABC is used in a program with the line

```assembly
ABC DB 3 ; ABC is of type byte
```

then a command such as

```assembly
NEG [ABC]
```

means the same thing as

```assembly
NEG BYTE PTR [ABC]
```

In NASM (and in Edlinas) programs, there is no type significance attached to db. Common embellishments of the simple syntax also work in both.

```assembly
db imm, immn, ...
```

where a sequence of one-byte numbers follows the db, stores a sequence of bytes into the object code file.

In Edlinas, it is also possible to use an integer multiplier on the left. For example, the following code stores zero into one hundred bytes of memory.

```assembly
.db 100 * 0
```

In NASM the same effect can be achieved using the code

```assembly
TIMES 100 db 0
```

### 6.5.2 Hand Coding of Instructions
Because a new processor often uses an instruction set which is the same as an old instruction set except for one or two new instructions, it is often worthwhile to use an old assembler to program a new processor. New instructions can be utilized by hand coding them. Open source advocates may well note that if the assembler were an open source program, it could simply be reprogrammed to handle the new instruction. But that is another question.

# Program 6.9

```assembly
; Using immediate storage to encode the CPUID instruction.
;	MOV EAX, 0
	db 0FH, 0A2H		; Immediate storage
```

### 6.5.3 Initializing Data
In C it is easy to get the impression that there is no difference between a declaration with an initialization such as

```c
char x = 2;
```

and a declaration followed by an assignment such as

```c
char x;
x = 2;
```

In fact, however, there is a difference. In the second case there is an implied processor instruction which stores the immediate value 2. In the first case, however, no processor instruction is implied. The storage indicated may be performed by storing the 2 at a program internal address by the assembler before the program is ever loaded.

# Program 6.10

```assembly
; Tiny Edlinas program which uses a label to access stored data.
;	MOV AL, [ABC]
	OUT [1], AL
	RET
ABC:	.db 3
```

# Chapter 7. THE STACK

The *stack* is a portion of memory which is shared with the operating system. It is used by programs for communication with subprograms, for temporary storage, and when making system calls. It is called the stack because it has a "last stored first retrieved" policy. It is in fact an example of the data structure that is called a stack. Because it is used by the operating system as well as by the programmer, it must be used responsibly. Misusing the stack is a very easy way to crash a program, or the whole system, if the operating system is unprotected.

## 7.1 Push and Pop Operations
The following figure shows the stack and the ESP register. This register has the job of keeping track of the stack. It does this by holding the address of the top of the stack. The SP in ESP stands for *stack pointer*.

Although the ESP is called a general register because it is accessible to the programmer like the registers EAX, EBX, etc., writes to ESP should be done only with great care.

Suppose that ESP contained the address 19H as in Figure 7-1. Then storing the byte 76H on the stack would fill the location 18H and the stack pointer would be changed, as shown in Figure 7-2. This kind of operation is called a push. The one-byte push shown here is essentially the same as the following two operations:

### Figure 7-1. Before Push

![](img/165a4f637c5eaccb372f5a82ca458a05_91_0.png)

### Figure 7-2. After Push

![](img/165a4f637c5eaccb372f5a82ca458a05_91_1.png)

```assembly
DEC ESP ; Move the pointer to the first vacancy.
MOV [ESP], 76H ; Store 76H at the address in ESP.
```

In fact, the x86 does not allow one-byte pushes. All pushes must be either two-byte or four-byte pushes. The number of bytes pushed is determined by the size of the operand on the PUSH instruction.

### 7.1.1 The PUSH Command
The most common form of the PUSH instruction is

```assembly
PUSH reg
```

Allowable registers include the 16- and 32-bit general registers, but not the eight-bit registers. Memory and immediate operands can also be used with PUSH, but the register operand form is the most useful.

Figure 7-3 and Figure 7-4 show the effect of a PUSH EAX instruction.

### Figure 7-3. Before PUSH EAX

![](img/165a4f637c5eaccb372f5a82ca458a05_92_0.png)

### Figure 7-4. After PUSH EAX

![](img/165a4f637c5eaccb372f5a82ca458a05_92_1.png)

This is very similar to

```assembly
SUB ESP, 4
MOV [ESP], EAX
```

Because the stack pointer points to the last occupied location rather than the first unoccupied location of the stack, a *PUSH* must be carried out by subtracting from the stack pointer first and then transferring the bytes to the stack rather than the other way around. Having the stack pointer point to the first available location would be a reasonable policy if all pushes and pops were the same size. But since pushes and pops may be either two or four bytes, this is not a tenable policy.

### 7.1.2 The POP Command
The opposite operation is called a *pop*. Like the *PUSH* instruction, *POP* takes register and memory operands, which may be either two or four bytes. Unlike *PUSH*, it does not take immediate operands. As with pushes, the size of the operand determines the number of bytes to be popped. Since BX is a two-byte register, *POP* BX pops two bytes off the stack.

```assembly
POP BX
```

This is very similar to

```assembly
MOV BX, [ESP]
ADD ESP, 2
```

One use for the stack is simply for storage when there are not enough registers available. Suppose there are values in EAX and EBX which are important and need to be saved, but that also a computation has to be done which uses the registers EAX and EBX. This is a situation which calls for using the stack. Before the computation is done, the values in the registers EAX and EBX may be saved on the stack. After the computation is finished, they may be restored again. The following code does this:

```assembly
PUSH EAX
PUSH EBX
...
; Computation
...
POP EBX
POP EAX
```

The order of the pops is the exact reverse of the order of the pushes. This is because of the "last stored first retrieved" character of a stack. The values in EAX and EBX at the end should be the same as at the beginning. But this will only be true if the intervening computation uses the stack responsibly. This means that each push should be matched with a pop. If pushes and pops are not balanced, then the values popped into EBX and EAX at the end of computation will not be the same as their original values.

When writing a user program to be run in Unix, it is not necessary to initialize the stack by storing a value in ESP. In fact, since the stack is already set up, storing an arbitrary value in ESP would disrupt the existing stack and crash the program. When writing a program to run in Edlinas, however, it is necessary to initialize ESP.

## 7.2 Subprograms
High-level programming languages use subprograms in order to reduce complex tasks to simpler components. In C, subprograms are functions. A function may be called as though it were another C instruction. If the function subpr() has been defined, then it may appear in a line of a main program, as in Program 7.1.

# Program 7.1

```c
main()
{
    int x, y, z;
    ...
    subpr(); // This subprogram is defined separately.
    ...
}
```

### 7.2.1 The CALL and RET Commands
Coding an assembler program which has a subprogram is done using the CALL and RET instructions. RET stands for return. These commands work like jump to and jump back commands. The format of the CALL instruction is very similar to the format of the JMP instruction.

# Program 7.2

```c
subpr()
{
    int a, b, c;
    ...
    return c;
}
```

```assembly
CALL label
```

As with the JMP instruction, the label is created by the programmer and refers to the line whose label field it occupies.

When the subprogram is done, control needs to be transferred back to the main program; in particular the next instruction executed in the main program needs to be the instruction following the CALL instruction. To make this possible, the processor pushes the address of the next instruction onto the stack before it leaves the
