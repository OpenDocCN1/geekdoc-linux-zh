
If you're sharp, the question will already have occurred to you: What about the flat models? Recall that in both real flat mode model and protected mode flat model, the segment registers all point to the same place and are not changed during the run of the program. In the flat models you do not use segment overrides. What I have explained previously about segment overrides applies only to the real segment model!

## Real Mode Memory Data Summary

Real memory data consists of a single byte or word in memory, addressed by way of a segment value and an offset value. The register containing the offset address is enclosed in square brackets to indicate that the contents of memory, rather than the contents of the register, are being addressed. The segment register used to address memory data is usually assumed according to a complex set of rules. Optionally, a segment override prefix may be placed in the instruction to specify some segment register other than the default segment register.

Figure 7.1 shows diagrammatically what happens during a MOV AX,[ES:BX] instruction. The segment address component of the full 20-bit memory address is contained inside the CPU in segment register ES. Ordinarily, the segment address would be in register DS, but the MOV instruction contains the ES segment override prefix. The offset address component is specified to reside in the BX register.

The CPU sends out the values in ES and BX to the memory system side by side. Together, the two values pin down one memory location where MyWord is actually two bytes, but that's fine—all the x86 CPUs working in real mode (except for the 8088) can bring both bytes into the CPU at once, while the 8088 brings both bytes separately, one after the other. The CPU handles details like that and you needn't worry about. Because AX is a 16-bit register, of course, two 8-bit bytes can fit into it nicely.

The segment address may reside in any of the four segment registers: CS, DS, SS, or ES. However, the offset address may reside only in registers BX, BP, SP, SI, or DI. AX, CX, and DX may not be used to contain an offset address during real mode memory addressing.

## Limitations of the MOV Instruction

The MOV instruction can move nearly any register to any other register. For reasons having to do with the limited budget of transistors on the 8086 and 8088 chips, MOV can’t quite do any move you can think of—in real mode, at least. Here’s a list of MOV’s real mode limitations:

- 1. MOV cannot move memory data to memory data. In other words, an instruction like MOV [SI],[BX] is illegal. Either of MOV’s two operands may be memory data, but both cannot be at once.
- 2. MOV cannot move one segment register into another. Instructions like MOV CS,SS are illegal. This could have been handy, but it simply can’t be done.
- 3. MOV cannot move immediate data into a segment register. You can’t code up MOV CS,0B800H. Again, it would be handy but you just can’t do it.
- 4. MOV cannot move one of the 8-bit register halves into a 16-bit register, nor vice versa. There are easy ways around any possible difficulties, and preventing moves between operands of different sizes can keep you out of numerous kinds of trouble.

These limitations, of course, are over and above those situations that simply don't make sense: moving a register or memory into immediate data, moving immediate data into immediate data, specifying a generalpurpose register as a segment register to contain a segment, or specifying a segment register to contain an offset address. Table 7.3 shows numerous illegal MOV instructions that illustrate these various limitations and nonsense situations.

## Some Notes on Assembler Syntax

Although we haven't talked about it a whole lot just yet, this book focuses on a particular assembler called NASM. And if this book is your first exposure to assembly language, nothing I've said so far would cause you any cognitive dissonance with your earlier experience, since you have no earlier experience. However, if you've played with assembly using other assemblers, you will soon begin to see small differences between what you learned in writing assembly language mnemonics and what I'm teaching in this book. These differences are matters of syntax, and they may become important, especially if you try to convert source code to NASM from another assembler such as MASM, TASM, or A86.

Table 7.3 Rogue MOV Instructions

| ILLEGALSTRUCTION | WHY IT'S ILLEGAL |
|---|---|
| MOV 17,I | Only one operand may be immediate data. |
| MOV 17,BX | Only the source operand may be immediate data. |
| MOV CX,DH | The operands must be the same size. |
| MOV [DI],[SI] | Only one operand may be memory data. |
| MOV DI,[DX:BX] | DX is not a segment register. |
| MOV ES,0B800 | Segment registers may not be loaded from immediate data. |
| MOV DS,CS | Only one operand may be a segment register. |
| MOV [AX],BP | AX may not address memory data (nor may CX or DX). |
| MOV SI,[CS] | Segment registers may not address memory data. |

![](img/5af1f694a521bb214c2fd03b770b346f_235_0.png)
Figure 7.1 How memory data is addressed.
