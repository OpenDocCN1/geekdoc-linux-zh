# ASSEMBLY LANGUAGE STEP-BY-STEP

It really is simple. The trick, as usual, is knowing what’s happening based on what you see on your screen. Without some preparation, nexti and stepi are pretty closed-mouthed and unhelpful. Stop at a breakpoint and execute nexti, and this is what you’ll see:

```
(gdb) nexti
0x0483d9 in main ()
```

The hex number is the 32-bit value of the program counter at that instruction. And that’s all you tell. You, however, instruct gdb to be a little more verbose. This is done with the display command, using the following syntax:

```
(gdb) display /i $pc
1: x/i $eip 0x0483d86 <main+6> movl 0x8(%ebp),%ecx
```

More like it! Here we have three major pieces of information: the machine address of the next instruction to be executed, the offset in instructions from the nearest label, and the machine instruction mnemonic, in AT&T format. The /i portion of the display command instructs gdb to display what it finds in memory as instructions, using gdb’s built-in disassembler. The $pc is a built-in symbol that specifies address to use in display: the address currently stored in the program counter register, EIP.

“1:” at the left margin is the identification number of this display format. It’s possible to have several display formats active at the same time, so that you can automatically display one or more registers or other items every execution pauses. For example, if you’re watching ECX, you might issue this display command as well:

```
(gdb) display /x $ecx
2: /x $ecx = 0x1
```

Now we have a second active display format, showing us the value of register ECX in hex format. Every time you issue the next command, you’ll see something like this:

```
(gdb) /x $ecx = 0x1
1: x/i $eip 0x0483d89 <main+9> movl 0xc(%ebp),%ebx
```

This way, you can watch the effects of executing instructions on registers or program variables as the program progresses.

Note that as you create new display formats, they stack up with the oldest at the bottom. If you want to delete a display format so that it doesn’t