```
db "Hello world!", 0AH,0
```

In order to call `scanf()` from assembler it is necessary to have a label in a data segment. The `scanf()` function takes user input and writes it into memory. This memory cannot be in the text segment. It must be in a data segment. Because `printf` and `scanf` occur as references to unknown locations, NASM requires the use of an `extern` directive. NASM will produce an error message if a label is referred to which does not occur in the label field of a line in the program being assembled. Program 8.5 shows how to call `printf()` and `scanf()` from a NASM program. A word of warning is in order regarding register usage. Although we might expect C library functions such as `printf()` and `scanf()` to save registers on the stack before using them, they don't necessarily. Values stored in registers before a call to `printf()` *need not* be there after this call. To preserve values from destruction by a library function call, the programmer must assume the responsibility of saving them on the stack. The lines labeled `ABC`, `BCD`, and `CDE` store strings. `XYZ` is located in the data segment. Consequently, the `MOV EAX, [XYZ]` instruction can execute without causing a memory violation.

# 8.5 Other Data Segments

Linux user memory is data space that is internal to the program itself. There are three kinds of data space internal to a program.

# Program 8.5

```
```
; This program calculates y = 2 * x + 1
section .text
global main
extern printf
extern scanf
main: PUSH ABC
CALL printf
ADD ESP, 4
PUSH XYZ
PUSH BCD
CALL scanf
ADD ESP, 8
MOV EAX, [XYZ]
ADD EAX, EAX
INC EAX
PUSH EAX
PUSH CDE
CALL printf
ADD ESP, 8
RET
ABC: db "Enter a number: ", 0AH,0
BCD: db "%d \x0" ,0AH,0
CDE: db "You get %d.\x0" ,0AH,0
section .data
XYZ: db 4 * 0
```
```

+   1. Initialized data space. It is space that is internal to the executable file, even when the file is lying idle out on the disk.
+   2. Uninitialized data space. It is space that is added to the program when the program is loaded.
+   3. Dynamically Allocated Memory. It is space that is added to the program when it is executing.

# 8.5.1 Initialized Data Space

In chapter 6, section 6.5.3 the use of the `db` directive was discussed in connection with the initialization of data. The fact that this data needs to be stored permanently requires that it be a part of the executable file.