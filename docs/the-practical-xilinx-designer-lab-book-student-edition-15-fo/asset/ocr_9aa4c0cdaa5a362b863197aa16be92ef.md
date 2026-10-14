![](bbox=[0.269, 0.043, 0.746, 0.344])

**Figure 10.1** Calling and returning from a subroutine.

The circuitry just discussed will work only if a single subroutine is called. But what if the subroutine calls another subroutine? This is called subroutine nesting. In this case, the SAVE register will be overwritten with an address from the subroutine code and the return address to the main program will be lost. Therefore, the microprocessor will not remember which address to return to after all the subroutines have finished. To support nesting of N subroutines, N multiple registers, (SAVE₁, SAVE₂, ..., SAVEₙ) must be built. Whenever a jsr instruction is executed, the following transfers of addresses occur:

```
SAVEₙ ← SAVEₙ₋₁

SAVE₂ ← SAVE₁
SAVE₁ ← PC₁
```

and the reverse operation occurs whenever a ret instruction is executed:

```
PC ← SAVE₁
SAVE₁ ← SAVE₂
⋮
SAVEₙ₋₁ ← SAVEₙ
```

The multiple SAVE registers form what is called a subroutine stack. Addresses are pushed on the stack whenever a jsr instruction is executed. These addresses are popped off the stack and into the PC whenever a ret instruction is executed. Microprocessors often store their stack in external RAM and use a dedicated register (called a stack pointer) to keep track of where the top of the stack is in memory.