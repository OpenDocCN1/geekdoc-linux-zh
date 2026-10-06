
code, by using the BYTE directive. This will force you to think a little more about what you're doing at every point that you do it; that is, right where you use variable names as instruction operands. Doing so may help avoid certain really stupid mistakes—like the ones I used to make all the time while I was working with MASM, most of which came out of trying to let the assembler do my thinking for me.

To me, this is a wonderful thing, and one of the main reasons I chose NASM as the focus of this book.

Now here's another case, one that NASM will assemble without a burp:

```
MOV BL, BYTE MixTag
```

This looks innocent enough until you remember that MixTag is actually 2 bytes (one word) in size, having been defined with the DW directive. You might think this is an error, because MixTag isn't the same size as BL.
 True enough—but the key is that there's no ambiguity. The assembler knows what you want, even if what you want is peculiar. The type specifier MixTag is not byte-sized, however, so what actually happens is that the least significant (lowermost) byte of MixTag will be loaded into BL, with the most significant byte left high and dry.

Is this useful? It can be. Is it dangerous? You bet. It is up to you to decide whether overriding the type of memory data makes sense and doing so completely your responsibility to ensure that doing doesn't sprinkle your code with bugs. But nothing is left for the assembler to decide. That's what type specifiers are for: to make clear to the assembler in every case what it is supposed to do. Whether that in fact makes sense is up to you. Use your head—and know what you're doing. That's more important in assembly language than anywhere else in computer programming.

# CHAPTER 8

# Our Object All Sublime

Creating Programs that Work

They don't call it "assembly" for nothing. Facing the task of writing an assembly language program brings to mind images of Christmas morning: You've spilled 1,567 small metal parts out of a large box marked Land Shark HyperBike (Some Assembly Required) and now you have to how put them all together with nothing left over. (In the meantime, the kids seem more than happy playing in the box ...)

I've actually explained just about all you must understand to create your first assembly language program. Still, there is a nontrivial leap from there there; you are faced with many small parts with sharp edges that can fit together in an infinity of different ways, most worst, workable, but only a few that are ideal.

So here's the plan: In the following section I will present you with the completed and operable Land Shark HyperBike—which I will then tear apart before your eyes. This is the best way to learn to assemble: By pulling apart programs written by those who know what they're doing. Over the rest of this book we'll pull a few more programs apart, in the hope that by the time it's over you'll be able to move in the other direction all by yourself.

# The Bones of an Assembly Language Program

The following listing is perhaps the simplest correct program that will do anything visible and still be comprehensible and expandable. This issue of comprehensibility is utterly central to quality assembly language programming. With no other computer language (not even APL or that old devil FORTH) is there anything even close to the risk of writing code that looks so much like something scraped off the wall of King Tut's tomb.

The program EAT.ASM displays one (short) line of text on your display:

At Joe's

For that you have to feed 28 lines of text file to the assembler. Many of those 28 lines are unnecessary in the strict sense, but serve instead as commentary to allow you to understand what the program is doing (or more important, how it's doing it) six months or a year from now.

One of the aims of assembly language coding is to use as few instructions as possible in getting the job done. This does not mean creating as a short code file as possible. (The size of the source file has nothing to do with the size of the executable file assembled from it!) The more comments you put in your file, the better you'll remember how things work inside the program the next time you pick it up. I think you'll find it amazing how quickly the logic of a complicated assembly language file goes cold in your head. After no more than 48 hours of working on other projects, I've come back to assembler projects and had to struggle to get back to speed on development.

Comments are neither time nor wasted. IBM used to say, One line of comments per line of code. That's good—and should be considered a minimum for assembly language work. A better course (that I in fact follow in the more complicated examples later on) is to use one short line of commentary to the right of each line of code, along with a comment block at the start of each sequence of instructions that work together in accomplishing some discrete task.

Here's the program. Read it carefully:

```
; Source name      : EAT.ASM
; Executable name : EAT.COM
; Code model      : Real mode flat model
```

```
; Version : 1.0
; Created date : 6/4/1999
; Last update : 9/10/1999
; Author : Jeff Duntemann
; Description : A simple example of a DOS .COM file programmed with
NASM-IDE 1.1 and NASM 0.98.
```

```
[BITS 16] : Set 16 bit code generation
[ORG 100H] : Set code start address to 100h (COM file)
```

```
[SECTION .text] : Section containing code
```

```
START:
```

```
mov dx, eatmsg : Mem data ref without [] loads the ADDRESS!
mov ah,9 : Function 9 displays text to standard output.
int 21H : INT 21H makes the call into DOS.
```

```
mov ax, 04C0H : This function exits the program
int 21H : returns control to DOS.
```

```
[SECTION .data] : Section containing initialized data
```

```
eat db "At Joe's!", 13, 10, "$" ;Here's our message
```

# The Simplicity of Flat Model

After all our discussion in previous chapters about segments, this program might seem, um... suspiciously simple. And it's simple, and it's almost entirely because it's written for the 16-bit real mode flat model. (I drew this out in Figure 6.8) The first thing you'll notice is that there are no references to segments or segment registers anywhere. The reason for this is that in real flat model, you are inside a single segment, and everything you do, you do within that single segment. If everything happens within one segment, the segments (in a sense) “factor out” and you can imagine that they don't exist. Once we assemble A.ASM and create a runnable program from it, I'll show you what segment registers are up to and how it is that you can most ignore them in real mode flat model.

But first, let's talk about what all those lines are doing.

At the top is a summary comment block. This text is for your use only. When NASM processes a .ASM file, it strips out and discards all text between any semicolon and the end of the line semicolon is in. Such lines are comments, and they serve only to explain what's going on in

your program. They add nothing to the executable file, and they don't pass information to the assembler. I recommend placing a summary comment block like this at the top of every source file you create. Fill it with information that will help someone else understand the file or that will help you later on, after it's gone cold in your mind.

Bene the comment block is a short sequence of commands directed to the assembler. These commands are placed in square brackets that NASM knows that are for its use, and are not to be interpreted as part of the program.

The first of these commands is this:

```
[BITS 16 ; Set 16 bit code generation
```

The BITS command tells NASM the program it's assembling is intended to be run in real mode, which is a 16-bit mode. Using [BITS 32] instead would have brought into play all the 32-protected goodies introduced with the 386 and later x86 CPUs. On the other hand, DOS can't protect mode programs, so that wouldn't be especially useful.

The next command requires a little more explanation:

```
[ORG 0100h ; Set code start address to 100h (COM file
```

“ORG” is an abbreviation of origin, and what it specifies begins called the origin of the program, where is code execution begins. Code execution begins 0100H for this program. The 0100H value (the h and H are interchangeable) is loaded into the instruction pointer IP by DOS when the program is loaded and run. So, when DOS turns control over to your program (scary thought, that!), the first instruction to be executed is the one pointed to by IP—in this case, at 0100H.

Why 0100H? Look back at Figure 6.8. The real flat model (which is often called .COM file) has a 256-byte prefix at the beginning of its single segment. This is the Program Segment Prefix (PSP) and it has several uses I won't be explaining here. The PSP is basically a data buffer and contains no code. The code cannot begin until after the PSP, so the 0100H value is there to tell DOS to skip those first 256 bytes.

The next command is this:

```
[SECTION .text] ; Section containing code
```