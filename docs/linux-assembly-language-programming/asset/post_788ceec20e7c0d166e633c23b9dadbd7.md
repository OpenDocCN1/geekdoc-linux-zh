
main program. CALL does this. The RET instruction pops this address off the stack and jumps to it.

For example, Program 7.3 is a program that accepts a user input, uses a subprogram which adds 1 to the EBX register to increment the number, and then outputs the result back to the user.

## **Program 7.3**

```asm
;           MOV ESP, 2000H ; initialize the stack
;           ; Eddinas programs must initialize the stack
;           ; Unix programs must not.
;
;           IN EAX, [0]      ; Get a user input
;           MOV EBX, EAX     ; EBX is where the subroutine works.
;           CALL subpr       ; Leave for the subroutine.
;           MOV EAX, EBX     ; Back now from the subroutine!
;           OUT [1], EAX     ; Output the incremented value
;           RET              ; Go back to Eddinas.
; subpr:
;           INC EBX          ; Subprogram does its job.
;           RET              ; Go back to the main program.
```

For a more involved example, consider the following algorithm. This algorithm is at the heart of a well-known, unsolved mathematics problem called the Collatz Problem.

- If x is even divide it by 2
- If x is odd multiply it by 3 and add 1 to it.
- Repeat this process until x = 1.

Suppose we want a program which executes this algorithm and counts how many steps are required until the value of x becomes 1.

Since it requires a loop to determine whether a number is even or odd, or to divide it by 2, if we are using only add, subtract, and conditional jump commands, it makes sense to devise a subprogram to do this. Specifically, suppose we assign the subprogram the task of examining the EAX register and storing half of EAX in EBX if EAX is even, and zero in EBX otherwise. We may code this subprogram as follows:

## **Program 7.4**

```asm
HAF: MOV ECX, EAX
     MOV EBX, 0
AGN: INC EBX      ; Count the subtractions
     SUB ECX, 2   ; Repeatedly subtract 2
     JG AGN       ;
     JZ DUN       ; It comes out even
     MOV EBX, 0   ; It's not even.
DUN: RET
```

With this subprogram we may now write a main program which executes Program 7.4.

### 7.3 Parameter Passing

One of the most important functions of the stack is that it is used for parameter passing. For example, suppose the character code converting function `tolower()` is called in a C program.

The `tolower()` function in the standard C library `ctype.h` converts the character codes to lower case. For example, on a machine using ASCII, code it will return 97, the ASCII code for 'a', if given 65, the ASCII code for 'A', as an input parameter. The input parameter is pushed onto the stack. So the assembler code for the same function call looks like this:

## **Program 7.5**

```c
#include <ctype.h>

main()
{
    int x, y;

    x = 65; /* x = 'A' */
    y = tolower(x); /* y = 'a' */
}
```

```asm
    MOV EBX,  65
    PUSH EBX
    MOV EDX,  0
    IN EAX, [DX]
ABC:  CMP EAX,  1         ;
      JE FIN              ;If EAX = 1 then it's over.
      INC EDX             ;Use EDX as the counter.
      CALL HAF            ;This is the subroutine call!
      CMP EBX,  0         ;EBX = 0 means EAX is odd
      JE ODD              ;
      MOV EAX, EBX        ;If not then EBX is half of EAX
      JMP ABC
ODD:  MOV EBX,  EAX       ;Triple EAX and add 1
      ADD EAX, EBX
      ADD EAX, EBX        ;
      INC EAX
      JMP ABC             ;
FIN:  MOV EAX,  EDX       ;EDX contains the final count.
      MOV EDX,  1
      OUT [DX], EAX
      RET
```

## **Program 7.6**

```asm
    CALL tolower
    ADD ESP, 4
```

Although it might seem like a natural idea to use the stack for the return value, it is more common to use a register. In gnu C for the x86, returned integer values are stored in the EAX register. Languages differ as to whether the subprogram or the main program is responsible for popping the parameters off the stack. In Fortran, Basic, and Pascal the subprogram pops the stack, but in C the calling program does. This is the reason for the `ADD ESP, 4` instruction in the calling programs just shown.

Languages also differ in the order in which parameters are pushed onto the stack. C pushes parameters starting from the right. Suppose we have defined an integer power function `ipow()`:

```c
    int ipow(int base, int exponent);
```

The assembler code to call this function to calculate $2^3$ looks like this:

```asm
    MOV EBX,  3
    PUSH EBX
    MOV EBX,  2
    PUSH EBX
    CALL ipow
    ADD ESP, 8
```

After this call, the result `ipow(2, 3) = 8` will be stored in the EAX register.

### 7.3.1 The Global Assembler Directive

In the `.o` files produced by the gnu compiler, symbols such as `printf` or `tolower` which need external linkage are coded differently in the symbol tables. Without this special coding the gnu linker will pass them by and linkage will fail. In order to receive this special encoding, the assembly language source code must specially indicate symbols which are to receive this treatment. There is an assembler directive recognized by the gnu assembler and by Edlinas which will cause the assembler to encode a symbol in the symbol table as available for linkage. Its syntax is:

```asm
.globl symbol
```

In NASM the syntax is:

```asm
global symbol
```

### 7.3.2 Calling Assembler from C

The `half` subprogram would not work if called from C because it does not return values in the `EAX` register. Also, it does not push the registers it uses. In the code below, `ECX` is pushed because it is used and the calling program could be using it for something else. We also need to make the function name visible using the `global` directive.

We have just written a function in assembler which we can call from a C program. The C program will store the calling parameter on the stack. It will be buried under the return address pushed by the calling program and the contents of `ECX` which were just pushed. These two items occupy eight bytes on the stack, so the calling parameter is accessed at the address `ESP` + 8. The result is stored in `EAX` instead of `EBX`. To save the object code as a `.o` file while in Edlinas, use the `o` key. To produce an object code file using NASM, enter:

## Program 7.7

```asm
        global half ; or    .globl in Edlinas
half:
        PUSH ECX        ; ECX is used, so push it.
        MOV ECX,  [ESP +  8]
                        ; Stack top + 2 integers

        MOV EAX,  0
        INC EAX         ; Count the subtractions
AGN:
        SUB ECX,  2     ; Repeatedly subtract 2
        JG AGN          ;
        JZ DUN          ; It comes out even
        MOV EAX,  0     ; It's not even.
DUN:
        POP ECX
        RET
```

```bash
$ linuxbox$ nasm -f elf half.asm
```

The `-f elf` switch specifies the format of the object code file which in current Linux is `elf`. This format is discussed further in chapter 8.

Program 7.8 is a C program which calls the function `half()` (whose assembly code is shown in Program 7.7). If Program 7.8 is saved in a file `collatz.c`, then to compile it and link it with `half()`, use `gcc` on both files:

```bash
$ linuxbox$ gcc collatz.c half.o
```

## 7.4 Recursion

In recursion, much of the work of computation is done by the parameter-passing mechanism.

A recursive definition can very often be easily turned into a computationally effective, if not efficient, program. This is typically illustrated using the Fibonacci numbers.

$$
fib(k) = \begin{cases}
1 & \text{if } k < 2 \\
fib(k - 1) + fib(k - 2) & \text{otherwise.}
\end{cases}
$$

Program 7.9 shows how this recursive definition can be turned into C code. In assembly language, we can code this easily, provided we recall that used registers other than EAX must be pushed. Program 7.10 shows how we can get by using only ECX and EAX. To test this program from C, one can use a small calling program such as Program 7.11. To test a program like this using Edlinas, it is also necessary to initialize the stack, as is shown in the first line of Program 7.3.

## Program 7.8

```c
main()
{
    int count, x, y;
    count = 0;

    printf("Enter a number:  ");
    scanf("%d", &x);

    while(x != 1)
    {
        count = count + 1;
        y = half(x); /* This is the subroutine call! */
        if(y != 0)
            x = y;
        else
            x = 3*x + 1;
        printf("\n x = %d.", x);
    }
    printf("\n There were %d iterations.\n\n.",count);
}
```

## Program 7.9

```c
int fib(int k)
{
    int d;

    if(k < 2)
        d = 1;
    else
        d = fib(k-1) + fib(k-2);

    return d;
}
```

## Program 7.10

```asm
    global fib
fib:    PUSH ECX          ; Gives us access to ECX
        MOV EAX, [ESP + 8]
                        ; Access parameter
        CMP EAX, 2          ; if k < 2
        JAE ELS           ;
        MOV EAX, 1        ; Put the return value in EAX
        JMP DUN
ELS:    DEC EAX           ; Get k-1
        MOV ECX, EAX      ; EAX will be overwritten!
```
