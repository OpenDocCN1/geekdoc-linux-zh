# Coding for Linux 507

The base pointer we already have EBX. The argument index for Arg(0) is 0, for Arg(1) is 1, and so on. The address for Arg(1) would be the base pointer plus 1 times 4—which points at the pointer to Arg(1). The address for Arg(3) would be the base pointer plus 3 times 4, or 12 bytes from the start of the table. As you can see in Figure 13.3, that's exactly where Arg(3) is. The way this encodes in NASM syntax is:

```
push dword [ebx+esi*4] ; Push address of an arg on the stack
```

We're pushing the pointer onto the stack here, but scaled addressing can be used anywhere you can use a memory address in assembly work. The important part of the notation is [EBX + ESI * 4]. This is the implementation of our addressing algorithm, and it's baked right into the silicon of the CPU!

I've written a short program that displays all the command-line arguments, and in doing so demonstrates how to use scaled addressing to get the address of any given argument. Read it carefully:

```
; Source name : SHOWARGS.ASM
; Executable name : SHOWARGS
; Version : 1.0
; Created date : 10/1/1999
; Last update : 12/3/1999
; Author : Jeff Demann
; Description : A demo shows how to access command line arguments
stored on the stack by addressing them relative to ebp.
```

```
; Build using these commands:
  nasm -f elf showargs.asm
  gcc showargs.o -o showargs
```

```
; To test, execute with some command-line arguments:
  ./showargs foo bar bas bat
```

```
[SECTION .text]

global main ; Section containing code
extern printf ; Required so linker can find entry point
; Notify linker that we're calling printf
```

```
main:
push ebp ; Set up stack frame for debugger
  mov ebp, esp
  push ebx ; Program must preserve ebp, esi, &edi
  push esi
  push edi
  ;; Everything before this is boilerplate; use it for all ordinary apps!
```