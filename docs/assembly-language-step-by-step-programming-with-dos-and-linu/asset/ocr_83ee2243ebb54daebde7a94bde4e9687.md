# Coding for Linux

down. NASM won't warn you if there is a local label with the same name on your side of a global label and you try to jump to a local label on the other side of the global label. Bugs like this can be insanely difficult to find sometimes. Like any tool, local labels should be used carefully to be of greatest benefit.

# Placing Constant Data in a Subroutine

Now you're used to thinking of code as living in the [.text] section and data as living in the [.data] section. In almost all cases this is a good way to organize things, but there's no absolute demand that you separate code and data in this way. It's possible to define data within a subroutine using NASM's pseudoinructions including DB, DW, and DD. I've created a useful subroutine that shows how this is done and is a good example of when to do it.

The subroutine allows you to issue some number of newline characters to standard output, specified by a value passed to the subroutine in EAX:

```
newline:
mov ecx,10          ; We need a skip value, which is 10 minus the
sub ecx,eax         ; number of newlines the caller wants.
add ecx, dword nl   ; This skip value is added to the address of
push dword ecx       ; the newline buffer nl before calling printf.
call printf          ; Display the selected number of newlines
add esp,4           ; Clean the stack
ret                 ; Go home
l db 10,10,10,10,10,10,10,10,10,10
```

The buffer nl contains 10 newline characters, followed by a null. It is a null-terminated string of newline characters, and you can pass all of—or any chunk starting in the middle and going to the end—to printf. If you pass the address of the beginning of the string, printf will output all 10 newlines, and your display will show by 10 lines. If you pass the address of the third newline, printf will output only 8 newlines, having skipped the first 2. If you only want printf to output a single newline, you must pass the address of the very last newline, so that the only things that printf actually sends to standard output will be the final newline and the null character.

All the trickery is in calculating the address to pass to printf. The algorithm: To output x newline(s), we need to skip 10 – x newline(s). This is why we load 10 into ECX and subtract EAX from the result-