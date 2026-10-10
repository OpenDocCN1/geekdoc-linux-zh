initiates a data section.

With these directives we can direct NASM to produce a .o file with both text and data sections. Adding these directives to Program 8.2 gives us Program 8.3, which will compile and run without crashing.

# Program 8.3

```
```
; Tiny program which increments a byte of stored data.
; 
global main
section .text
main: MOV AL, [XYZ]
    INC AL
    MOV [XYZ], AL
    RET
section .data
XYZ: db 3
```
```

# 8.4.6 Segments in C Code

Program 8.4 can be used to determine the addresses of pages allocated to itself.

# 8.4.7 Calling C from Assembler

Calling functions involves using the stack. When functions are called using assembler, it is possible to see exactly how the stack is used in a function call. Once you know how to use the stack to call a function, you can call C library functions to get actual input and output for assembler programs which run under Linux.

In order to call printf() and scanf() using assembler, it is necessary to push strings onto the stack. This is because the first argument of each of these functions is always a string. The db assembler directive introduced in chapter 6, section 6.5.1 can be used to store strings as well as numbers. For example,

```
.db "Hello world!\n\x0"
```

can be used to store a string. If the location is labelled, then the label may be used to push the address of the stored string. In Edlinas the allowable strings are exactly like those allowed in the C language except that null termination must be explicitly encoded if it is desired. The C language hex escape sequence \x may be used to include a null or any other character into the string.

# Program 8.4

```
```c
char a = 'A';
main()
{
 char *n;
 int i,t;

n = &a;
printf("Enter a pointer displacement in hex:");
scanf("%x", &i);
printf("Pointer value in hex = %x\n", (n + i));
printf("Read, write, or skip? (Enter 0, 1, or 2):");
scanf("%d", &t);
if (t == 0)
 printf("Contents there= %x", *(n + i));
else if (t == 1)
*(n + i) = 'Y';
printf("\n");
}
```
```

In NASM, non-ASCII characters are coded outside the string using commas.