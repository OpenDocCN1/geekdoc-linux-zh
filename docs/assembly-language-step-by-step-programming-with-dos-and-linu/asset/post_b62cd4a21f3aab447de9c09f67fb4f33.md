
4. EAT.COM is the name of the output file. You can call the generated code file anything you want. If you don't specify the name of the output file, NASM will just lop off the “ASM” and call the file EAT. Unfortunately, the name “EAT” doesn’t indicate to DOS that it’s a runnable program, DOS won't know what to do with it. That's why you have to specify the full output file name “EAT.COM” on the command line.

Later on in this book, we're going to invoke NASM from the command line to produce a type of file that NASM-IDE won't be able to tell NASM how to produce. Therefore, we'll have to do it ourselves.

## What Happens When a .COM File Runs

It's useful to know what happens when you run a program of your own creation. DOS treats its two kinds of executable programs a little differently when you run them. .COM files are the simpler of the two. (I speak of .EXE files later in this chapter.) .COM files are a simple image of the instructions and data assembled from the source code file. When you execute a .COM program from the DOS command line, here's what happens:

- 1. The .COM file is loaded into memory at a location of DOS’s choosing. It doesn't change the file when it loads the file; the file is loaded exactly as it was saved to the assembler.
- 2. AX, DX, BP, SI, and DI are set to 0.
- 3. The instruction pointer IP is set to 0100H.
- 4. The number of bytes loaded from disk and stored into memory is placed in the CX register.
- 5. The stack pointer is set to the highest address in the program’s segment, minus one.
- 6. All four segment registers CS, SS, DS, and ES are set to the same value: the segment of the single segment in which the .COM program must run. DOS chooses this value.
- 7. DOS transfers control to the instruction at CS:IP, and your program is off and running!

You can see this very plainly by loading EAT.COM with DEBUG. Here's a dump of the registers immediately after loading EAT.COM into memory:

```
-E
AX=0000 BX=0000 CX=0001 DX=FFFF SP=0000 SI=0000 DI=0000
DS=1470 ES=1470 SS=1470 CS=1470 IP=0100 NV UP EI EL PL NZ NA PO NC
1470:0100 BA0C01 MOV DX, 010C
```

You'll sometimes hear the real flat model referred to as Tiny model. This is a term that originated in the C programming community, which has replaced separate names for several different arrangements of code and data, depending on whether there is a single segment for code or data or multiple segments.

The real flat model is itself—so simple, in fact, that it doesn't teach you much about segments. Maybe you don't need to know much about segments to craft useful programs these days (especially in protected mode flat model), but I've found it very useful to know how our CPUs evolved, and segments are a big part of. So, that said, let's look at EAS.ASM crafted for the real segmented model.

## One Program, Three Segments

The main problem with real flat model is that everything you must fit into 64K of memory. This isn't much of a pinch for learning assembly language and just playing around writing small utilities, but once you try to create something ambitious—say, a word processor or database-driven e-mail client—you find that code and data begin to crowd one another in a big hurry. So, for all its trouble, real mode segmented model was the only way to make full use of real mode's megabyte of memory.

Today, of course, you'd either create a Windows application (which would probably not attempt in assembly) or you'd work in protected mode flat model under an implementation of Unix for the Intel x86 CPUs. Nonetheless, if you understand segments, you have it in yourself to understand every other aspect of assembly work.

Let's do the Land Shark HyperBike trick again, this time with a version of EAS.ASM specifically written to use the real segmented model. Here's the bike—and then we'll take it apart just like last time:

- Source name : EATG.ASM
- Executable name : ESEG.EXE
- Code model : Real mode segmented model
- Version : 1.0
- Created date : 9/10/1999

## Our Object All Sublime

; Last update: 9/10/1999
; Author: Jeff Duntemann
; Description: A simple example of a DOS .EXE file programmed for
real mode segmented model, using NASM-IDE 1.1,
ASM 0.98, and ALINK. This program demonstrates
how segments are defined and initialized using NASM.

```asm
[BITS 16]

: Set 16 bit code generation

SEGMENT junk : Segment containing code

..start: The two dots tell the linker to Start Here.
; Note that this is a special symbol and MUST
; be in lower case! "..start: "..START:"

; SEGMENT SETUP

In real mode program uses three segments, and it must
set up the addresses in the three corresponding segment registers.
it is what the ASSUME directive does in NASM; ASSUME nothing in NASM!
Each of the three segments has a name (code, data, and stack) and
these names are identifiers indicating segment addresses. It is the
appropriate segment address that is moved into each segment register;
Note that you cannot move an address directly into a segment register;
you must first move the address into a general purpose register. Also
; note that we don't define anything with CS; the ..start: label tells the
; linker where the code segment begins.

```asm
mov ax,data ; Move address of data segment into AX
mov ds,ax ; Copy address from AX into DS
mov ax,stack ; Move address of stack segment into AX
mov ss,ax ; Copy address from AX into SS
```

```asm
mov sp,topstack ; Point SP to the top of the stack
```

```asm
mov dx,eatmsg ; Mem data ref without [] loads the ADDRESS!
mov ah,9 ; Function 9 displays text to standard output.
int 21H ; INT 21H makes the call into DOS.
```

```asm
mov ax,0C00H ; This DOS function exits the program
int 21H ; and returns control to DOS.
```

SEGMENT data ; Segment containing data

```asm
eatmsg db "Eat at Joe's", 13, 10, "$":Here's our message
```

SEGMENT stack ;This means a segment of type

```asm
resb 64 ; Reserve 64 bytes for the program stack
stacktop: ; It's significant that this label points to
the last of the reserved 64 bytes, and

### ASSEMBLY LANGUAGE STEP-BY-STEP

### Three Segments

Assembly language programs written for real mode segmented model must contain at least three segments: One for code, one for data, and one for the stack. Larger programs may contain than one segment and more than one data segment, but real programs may contain only one segment at a time.

EATSEG.ASM has three necessary segments. Each segment has a name: *stack*, *data*, and *code*, which indicate pretty clearly what the segment is. The *code* segment, pretty obviously, contains the machine instructions that do the program's work. The *data* segment contains initialized variables.

The stack segment contains the program's stack. I haven't explained stacks just yet, and you don't really need to understand stacks in order to understand how EATSEG.ASM, I'm going to hold off just a little longer. In short, a stack is simply an ordered place to stash things for the short term—and that will have to do until we cover the concept in depth in the next section.

Each of the three segments is declared using the SEGMENT directive, which is a command that tells NASM that a segment begins. The SEGMENT directive must be followed by the segment's name. You can name the segments whatever you like, custom suggests when you have only three segments, they are called *stack*, *data*, and *code*.

The segment containing the stack has some special considerations attached to it, especially regarding the linking of several files into one executable program. One of these considerations is that the stack have the type "stack" attached to it. This tells the linker (as I explain later) that this particular segment is special—it's a segment and not just a data segment. Hence the line:

```asm
SEG stack stack
```

Nobody's stuttering here. The SEGMENT directive is creating a stack named "stack" that is of the type "stack." The first identifier is the name;
