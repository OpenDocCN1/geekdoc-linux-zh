the second is the type. You could change the name of the segment to My-Stack or GreasedPig if you like, but it's important to let the type of the stack segment be precisely stack. More on this after we explain something else.

# Don't ASSUME...

If you remember, in the real flat model, the operating system sets all four segment registers to the same value (one that it selects) when the program is loaded into memory and run. In the real segmented mode, the different segments are indeed different and distinct regions of memory and are not all the same place. When the program begins running, DOS doesn't set the segment registers to anything. Your program must do that on its own. (DOS does, of course, set CS to the start of the code segment before giving control to your program. The other segment registers it leaves alone.)

This is what the first part of EATSEG.ASM does: It takes the addresses represented by the segment names for data and stack loads into DS and SS, the segment registers governing those segments:

```
mov ax,data      ; Move address of data segment into AX
mov ds,ax        ; Copy address from AX into DS
mov ax,stack     ; Move address of stack segment into AX
mov ss,ax        ; Copy address from AX into SS
```

Keep in mind that you can only load a segment register from a general-purpose register—you can't load it from anything, either data or memory data. This is why the segment addresses have to pass through AX to get into DS and SS. (Because we're not using ES to govern a segment defined at assembly time right there in our program, we don't need to load ES with anything off the bat.)

This is a good place to point out a crucial difference between NASM (the assembler that we are using in this book) and Microsoft's extremely popular MASM, which is probably the most-used assembler in history: MASM attempts to associate segment names with segment types. MASM does not.

With one small exception does a courtesy to the linker, NASM does not know which segment is the code segment, nor which segment is the data segment, nor which segment is the stack segment. You define a segment by name:

```
SEGMENT data      ; Segment containing initialized data
```