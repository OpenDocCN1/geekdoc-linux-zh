in our case is the startup/shutdown code from the C library) the shutdown values those registers had when the startup code called your program as the function main.

But once EBX, ESI, and EDI are there, you can push and pop whatever you need to for temporary storage. Calling C functions requires a fair amount of pushing and popping, as we see shortly.

# Destroying a Stack Frame

Before your program ends its execution by returning control to the startup/shutdown code (refer back to Figure 12.2 if this relationship isn't clear), its stack frame must be destroyed. This sounds to many like something wrong is happening, but not so: The stack frame must be destroyed, or your program will crash. "Put away" might be a better term than "destroyed" . . but let it pass. What we must do is leave the stack and the sacred registers in the state they when your program received control from the startup code.

Your stack must be clean before you destroy the stack frame and return control. This means that any temporary values that you have pushed onto the stack during the program's run must be gone. All that is left on the stack should be the caller's EBP, EBX, ESI, and EDI values on the stack, ESP (the stack pointer) had better be pointing to that saved EDI value, or there will be trouble.

Once your stack is clean, to destroy the stack frame you must first pop the caller's register values back into their registers, making sure your pops are in the correct order. Handing back the caller's EBX value in EDI will still crash your program! With that, we use the logic we followed in creating the stack frame: We restore the caller's ESP by moving the value from EBP to ESP, and finally pop the caller's ESP value off the stack:

```
mov esp,ebp
pop ebp
```

That's it! The stack frame is gone, and the stack and sacred registers are now in the same state they were in when the startup code handled to our program. It's now safe to execute the RET instruction that sends control to the shutdown code from the C library.

The file BOILER.ASM I showed earlier (it's on the CD-ROM for this book) is a boilerplate Linux assembly language program. It has a com-