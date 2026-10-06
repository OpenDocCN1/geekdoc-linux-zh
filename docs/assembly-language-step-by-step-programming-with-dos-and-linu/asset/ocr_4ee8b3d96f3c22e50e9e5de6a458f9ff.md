# Defining Macros with Parameters

So far, macros may seem useful but perhaps not especially compelling. What makes macros really sing is their ability to mimic high-level language subroutines and take arguments through parameters. For example, if you were to define a macro named GotoXY that would position the hardware cursor, you could pass it the X and Y values as arguments, separated by a comma:

```
GotoXY 17,3      ; Move the cursor to the Name field
```

You'd have to pinch yourself to be sure you aren't working in Basic, no? Macro parameters are, again, artifacts of the assembler. They are not pushed on the stack or set to COMMON or anything like that. The parameters are simply placeholders for the actual values (called arguments) that you pass to the macro through its parameters.

I've converted the GotoXY procedure to a macro to show how this works. Here's the macro:

```
@macro GotoXY 2      ; NewX, NewY
mov DH, %2          ; The NewY parameter loads into DH
mov DL, %1           ; The NewX parameter loads into DL
mov AH, 02H         ; Select VIDEO service 2: Position cursor
mov BH, 0           ; Stay with display page 0
int 10H             ; Call VIDEO
endmacro
```

So where are the parameters? This is another area where NASM differs from MASM. MASM allows you to use symbolic names—such as the words NewX and NewY—to stand for parameters. NASM relies on a simpler system that declares the number of parameters, and refers to the parameters by number rather than symbolic name.

In the definition of macro GotoXY, the number 2 after the name of the macro indicates that the assembler is to look for two parameters. This number must be present—as 0—even when you have a macro with no parameters. Later in the macro, the two parameters are referenced by number. "%1" indicates the first parameter used after the name "GotoXY," and "%2" indicates the second parameter:

```
GotoXY 11,14
Name %1 %2
```

I call the two parameters NewX and NewY—but they don't exist anywhere in the code! They're strictly creatures of the imagination to help me