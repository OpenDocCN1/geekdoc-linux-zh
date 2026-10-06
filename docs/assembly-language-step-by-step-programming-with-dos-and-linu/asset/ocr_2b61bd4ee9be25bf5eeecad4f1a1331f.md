we need to somehow tell DEBUG that it needs to save more than 13H bytes out to disk. To do this we need to look at and change a value in one of the CPU registers.

Registers, if you recall, are special-purpose memory cubbyholes that exist inside the CPU itself, rather than in memory chips outside the CPU. DEBUG has a command that allows us to examine and change register values as easily as we examine and change

At the prompt, type R. (Think, Registers.) You'll see a display like

```
AX=0000 BX=0000 CX=0014 DX=0000 BP=0000 SI=0000 DI=0000
DS=1980 ES=1980 SS=1980 CS=1980 IP=0100 NV UP EI PL NZ NA PO NC
1980:0100 53 PUSH BX
```

The bulk of the display consists of register names followed by equal signs, followed by the current values of the registers. The cryptic characters NV UP EI PL NZ NA PO NC are the names of flags; we discuss them later in the book.

The line beneath the register and flag summaries is a disassembly of the byte at the address contained by the instruction pointer. (The instruction pointer is a register which is displayed by the DEBUG R command, under the shorter name IP. IP's value in the preceding register display—it should be 010H, which is also the address of the "S" in "Sam.") This line will be useful when you're actually examining an executable program file. In the case of SAM.TXT, the disassembly is misleading, because SAM is not an executable program and contains nothing we intend to use as machine instructions.

The hexadecimal 53H, is a legal machine instruction—just as it is the ASCII code for uppercase S. DEBUG doesn't know what kind of file SAM.TXT is. SAM could be a program file as a text extension. DEBUG examines memory at the current address and displays it as though it were a machine instruction. If memory contains instead of machine instructions, the disassembly line should be ignored, even though it will always be there.

This is once again an example of the problems you can have in assembly language if you don't know exactly what you're doing. Code and data look the same in memory. They are only different in how you inter-