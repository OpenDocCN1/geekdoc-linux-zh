
![](img/165a4f637c5eaccb372f5a82ca458a05_0_0.png)

## Linux Assembly Language Programming

**Bob Neveln**  
**Publisher: Prentice Hall PTR**

First Edition July 21, 2000  
ISBN: 0-13-087940-1, 272 pages

Master x86 assembly language from a Linux perspective!  
Essential information for creating Linux device drivers!  
How Linux works "under the hood!"  
CD-ROM includes edlinas, the #1 Linux x86 hands-on assembler development simulator!

![](img/165a4f637c5eaccb372f5a82ca458a05_0_1.png)

*Linux Assembly Language Programming* is the first Linux-centered guide to x86 assembly language!

In *Linux Assembly Language Programming*, Bob Neveln explains all the key features of x86 assembly language in the context of the Linux operating system and the C language. The book’s step-by-step, one-concept-at-a-time coverage will help any hardware programmer move to Linux, and master essential skills for Linux device driver development. You won’t just learn new x86 assembly language skills; you’ll also gain powerful "under the hood" insight into how Linux works. Bonus CD-ROM includes edlinas, the #1 Linux-based x86 interactive assembler development simulator! This is Linux x86 assembly language programming, from start to finish:

-   Place-holding numeration
-   Logic circuits
-   Computation
-   The four-field format
-   Machine language
-   Memory
-   The stack
-   Linux user programs
-   NASM
-   DOS programs
-   Interrupts
-   Bit manipulations
-   Device drivers
-   And more...

-   Front Matter
-   Table of Contents
-   About the Author

© 2000 by Prentice-Hall

Published by Prentice Hall PTR

Prentice-Hall, Inc.

Upper Saddle River, NJ 07458

Prentice Hall books are widely used by corporations and government agencies for training, marketing, and resale.

The publisher offers discounts on this book when ordered in bulk quantities. For more information, contact: Corporate Sales Department, Phone: 800-382-3419; Fax: 201-236-7141; E-mail: corpsales@prenhall.com; or write: Prentice Hall PTR, Corp. Sales Dept., One Lake Street, Upper Saddle River, NJ 07458.

All products or services mentioned in this book are the trademarks or service marks of their respective companies or organizations. Screen shots reprinted by permission from Microsoft Corporation.

All rights reserved. No part of this book may be reproduced, in any form or by any means, without permission in writing from the publisher.

Printed in the United States of America

10 9 8 7 6 5 4 3 2 1

Prentice-Hall International (UK) Limited, *London*

Prentice-Hall of Australia Pty. Limited, *Sydney*

Prentice-Hall Canada Inc., *Toronto*

Prentice-Hall Hispanoamericana, S.A., *Mexico*

Prentice-Hall of India Private Limited, *New Delhi*

Prentice-Hall of Japan, Inc., *Tokyo*

Prentice-Hall Asia Pte. Ltd.

Editora Prentice-Hall do Brasil, Ltda., *Rio de Janeiro*

### **Credits**

**Editorial/production supervision:**

*Vincent Janoski*

**Acquisitions editor:**

*Miles Williams*

**Marketing manager:**

*Kate Hargett*

**Manufacturing manager:**

*Alexis Heydt*

**Cover design director:**

*Jerry Votta*

**Cover designer:**

*Nina Scuderi*

> *This book is dedicated to all imprisoned Plowshares activists for attempting to do with iron what also needs to be done with silicon.*

## Linux Assembly Language Programming

**PREFACE**

-   1. INTRODUCTION
    -   1.1 The Fetch-Execute Cycle
    -   1.2 The Linux Operating System
    -   1.3 The Gnu C Compiler
    -   1.4 The Eclinas Assembler
    -   1.5 NASM
    -   1.6 Other Assemblers
-   2. PLACEHOLDING NUMERATION
    -   2.1 The Decimal and Pentimal Systems
    -   2.2 Pentimal Arithmetic
    -   2.3 Conversion to Pentimal
    -   2.4 The Binary System
    -   2.5 Memory as a Rectangle of Bits
    -   2.6 The Hexadecimal System
    -   2.7 Base Distinguishing Notations
    -   2.8 * Fractions in Other Bases
    -   2.9 * Converting Fractions
-   3. LOGIC CIRCUITS AND COMPUTATION
    -   3.1 The NOT Gate
    -   3.2 Boolean Operators
    -   3.3 Logic Gates
    -   3.4 Addition Circuits
    -   3.5 Sequential Circuits
    -   3.6 Negative Number Representation
    -   3.7 Subtraction Using Negation
    -   3.8 * Placeholding Two's Complement
    -   3.9 Memory Circuits
    -   3.10 x86 General Registers and their Ancestry
    -   3.11 The MOV Command
    -   3.12 Addition and Subtraction Commands
    -   3.13 * Multiplication and Division Commands
-   4. ASSEMBLY LANGUAGE
    -   4.1 The Four Field Format
    -   4.2 Computers from the CPU Standpoint
    -   4.3 Simple Assembly Language Programs
    -   4.4 Assembler Programs with Jumps
    -   4.5 Assembler Programs with Loops
    -   4.6 Signed Comparisons
    -   4.7 Unsigned Comparisons
    -   4.8 Linux .s files
-   5. MACHINE LANGUAGE
    -   5.1 Assembling Simple Programs
    -   5.2 Opcode Space
    -   5.3 The ModRM Byte
    -   5.4 386 Space (OF + ...)
    -   5.5 32-Bit vs. 16-Bit Code
    -   5.6 The 8-Bit Registers
    -   5.7 Linux .o Files
-   6. MEMORY
    -   6.1 4-Byte Data Width
    -   6.2 Addresses in Brackets
    -   6.3 Operand Size Ambiguity
    -   6.4 Labels
    -   6.5 Immediate Storage
-   7. THE STACK
    -   7.1 Push and Pop Operations
    -   7.2 Subprograms
    -   7.3 Parameter Passing
    -   7.4 Recursion
-   8. LINUX USER PROGRAMS
    -   8.1 Multitasking
    -   8.2 Paging
    -   8.3 Address Translation
    -   8.4 Program Segments
    -   8.5 Other Data Segments
    -   8.6 I/O Protection
    -   8.7 Executable Files in ELF Format
    -   8.8 Object Files in ELF Format
-   9. INTERRUPTS
    -   9.1 Polling
    -   9.2 External Interrupts
    -   9.3 ISA Architecture
    -   9.4 Internal and Software Interrupts
    -   9.5 System Calls
    -   9.6 Privilege Levels
    -   9.7 Control Transfer
    -   9.8 Scheduling
-   10. BIT MANIPULATIONS
    -   10.1 Bitwise Logic Operations
    -   10.2 The AND, OR, NOT, and XOR Commands
    -   10.3 Bit Setting and Testing
    -   10.4 Shift Instructions
-   11. DEVICE DRIVERS
    -   11.1 Device-Independent Files
    -   11.2 Devices as Files
    -   11.3 Morse Code Speaker Driver
    -   11.4 Serial Port Digitizer Driver
-   12. DOS PROGRAMS
    -   12.1 Real Mode Segmentation
    -   12.2 Edlinas Environment Variables
    -   12.3 Fixed Memory Areas
    -   12.4 Real Mode Interrupts
    -   12.5 Checking DOS Memory
-   13. LINUX BOOT TIME PROGRAMS
    -   13.1 Changing to Protected Mode
    -   13.2 Protected Mode Segmentation
    -   13.3 Setting Up the Global Descriptor Table
    -   13.4 Closing

### PREFACE

Assembly language is the language which gives the programmer direct control over the computer. That is what appeals to people about assembly language. It is like using a stick shift. Programming with other languages, high-level languages, is like using an automatic.

Many people who use computers simply run programs. To them a program is a canned software package. People who like to write programs like to be able to shape the behavior of the machine the way metalsmiths shape metal into useful mechanical tools. Amongst all the programs on a computer, there is one program which runs the operating system. It controls everything. It offers "services" to the other programs. Most operating systems force programmers to leave their programming skills behind as they approach the operating system and to use it as they would a canned software package. That is because its source code is a secret. Linux portends the end of secret code in computing. Because the Linux source code and a compiler for it are right there on the computer along with the other source code, it allows programmers to work with the operating system as they do with programs they have written.

Operating systems were once written by programmers employed by computer manufacturers. Revolutions in hardware produced corresponding revolutions in the software. When Linus Torvalds rewrote Linux so that it would run on the Alpha architecture, his goal was not to increase its hardware base from one platform to two, but to make Linux platform-independent. The subsequent ports of Linux, to everything from a Sparc to a PowerPC, demonstrate the success of his rewrite. The chief value of it is that it provides us with confidence that Linux is here to stay. We don't have to fear a PowerPC revolution coming along and forcing us to dump all of our old software.

Assembly code, on the other hand, is intrinsically platform-dependent and is justifiably regarded with caution for just this reason. It will have to be redone when the next hardware revolution takes place. Furthermore, people who compare the machine language of the 386 with other machine languages, both real and ideal, inevitably end up regarding the 386 language as a historical accident. On the other hand, the genetic code is sometimes referred to as a *frozen accident*. The term is based on the idea that the genetic code ceased its evolution when the number of proteins whose code could be "broken" by a mutation in the genetic code became so large that such mutations became lethal, and so the code became fixed. It remains to be seen whether 386 machine code has been "frozen" into place by the size of its software base. The threat of a PowerPC revolution has passed. On the other hand, many Linux enthusiasts anticipate an Alpha revolution.

But the Alpha revolution has not happened and it may not happen. The 386 language has been around for a long time. With many RISC machines now emulating the 386 architecture, isn't it time to consider programming in 386 assembly language? Assembly language is more work but it has its advantages. A very nice feature of assembly language code, which it shares with Linux itself incidentally, is that from a crass performance standpoint, it functions beautifully. Relying on compilers to produce good code is usually justifiable as a time saving measure. But to get the best possible code, there is still no better option than to use assembly language. When high-level languages were still a novelty and referred to as *automatic programming*, many programmers were greatly offended by them. They were convinced that no computer program could write code as well as they could. They were right of course. Compilers produce cheaper code but not better code. To get the full measure of speed and grace that a machine is capable of, there is no substitute for assembly language.

Furthermore, even if the Alpha revolution arrives on schedule tomorrow, there will remain in the world millions of processors running a 386 language, which work beautifully and need to be put to a socially responsible use.

Computers can be programmed to report on our buying habits or to send off nuclear missiles. But they can also be programmed to communicate with privacy or to support medical research. As siliconsmiths, our job is to shape the behavior of the machine towards a human agenda.

This book assumes that the reader has some knowledge of C, but it makes no other assumptions.

Starred sections of the book are not needed subsequently and may be skipped when they are not of intrinsic interest.

I owe thanks to Dave Felter for writing a partial simulator of the 8080. This simulator got me started writing Edinas.
