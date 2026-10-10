# 7.3.1 The Global Assembler Directive

In the `.o` files produced by the gnu compiler, symbols such as `printf` or `tolower` which need external linkage are coded differently in the symbol tables. Without this special coding the gnu linker will pass them by and linkage will fail. In order to receive this special encoding, the assembly language source code must specially indicate symbols which are to receive this treatment. There is an assembler directive recognized by the gnu assembler and by Edlinas which will cause the assembler to encode a symbol in the symbol table as available for linkage. It's syntax is

```
```
.globl symbol
```
```

In NASM the syntax is:

```
```
global symbol
```
```

# 7.3.2 Calling Assembler from C

The `half` subprogram would not work if called from C because it does not return values in the `EAX` register. Also, it does not push the registers it uses. In the code below, `ECX` is pushed because it is used and the calling program could be using it for something else. We also need to make the function name visible using the `global` directive.

We have just written a function in assembler which we can call from a C program. The C program will store the calling parameter on the stack. It will be buried under the return address pushed by the calling program and the contents of `ECX` which were just pushed. These two items occupy eight bytes on the stack, so the calling parameter is accessed at the address `ESP` + 8. The result is stored in `EAX` instead of `EBX`. To save the object code as a `.o` file while in Edlinas, use the `o` key. To produce an object code file using NASM, enter

# Program 7.7

```
```
        global half ; or    .globl in Edlinas
half:
        PUSH ECX        ; ECX is used, so push it.
        MOV ECX,  [ESP +  8]
                          ; Stack top + 2 integers

        MOV EAX,  0
        INC EAX           ; Count the subtractions
AGN:
        SUB ECX,  2       ; Repeatedly subtract 2
        JG AGN            ;
        JZ DUN            ; It comes out even
        MOV EAX,  0       ; It's not even.
DUN:
        POP ECX
        RET
```
```

```
```
$ linuxbox$ nasm -f elf half.asm
```
```

The `-f elf` switch specifies the format of the object code file which in current Linux is `elf`. This format is discussed further in chapter 8.

Program 7.8 is a C program which calls the function `half()` (whose assembly code is shown in Program 7.7. If Program 7.8 is saved in a file `collatz.c`, then to compile it and link it with `half()`, use `gcc` on both files

```
```
$ linuxbox$ gcc collatz.c half.o
```
```

# 7.4 Recursion

In recursion, much of the work of computation is done by the parameter-passing mechanism.