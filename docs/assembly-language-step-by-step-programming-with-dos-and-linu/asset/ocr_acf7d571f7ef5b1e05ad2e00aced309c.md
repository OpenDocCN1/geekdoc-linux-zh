the end of the last chapter, when we found the JMP instruction that reboots your PC on power-up, and used G to execute that instruction. The command is quite evocative: Go. But don't type G just...

Here's the reason: You haven't entered a program. You've entered one instruction, and one instruction does not a program make. The instruction after your MOV instruction could be anything at all, recalling that DEBUG is simply interpreting garbage values in memory as random machine instructions. A series of random machine could easily go berserk, locking your system into an endless loop or writing zeroes over an entire segment of memory that may contain part of DOS or Windows, or of DEBUG itself. We'll use DEBUG'S G command a little later, once we've constructed a complete program in memory.

Go executes programs in memory starting at CS:IP; Trace executes the single instruction at CS:IP.

For now, let's consider the mechanism DEBUG for executing one machine instruction at a time. It's called Trace, and you invoke it by typing T The Trace command will execute the machine instruction at CS:IP, then give control of the machine back to DEBUG. Trace is generally used to single-step a machine-code program one at a time, in order to watch what's up to every step of the way. For now, it's a fine way to execute a single instruction and examine the instruction's effects.

So type T DEBUG will execute the MOV instruction you entered at CS:IP, and then immediately display the registers before returning to the dash prompt. You'll see:

```
AX=0000 BX=0000 CX=0000 DX=0000 SP=FFEE BP=0000 SI=0000 DI=0000
DS=1980 ES=1980 CS=1980 IP=0103 NV UP EI PL NA PO NC
1980:0103 6E DB 6E
```

Look at the first line. DEBUG says AX is now equal to 0001. Held the default value 0000 before; obviously, your MOV instruction worked.

And there's something else to look at: The third line shows an instruction called DB at CS:IP. Not quite true—DB is not a machine instruction, but an assembly language directive that means Define Byte. DB has other uses, but in this case it's simply DEBUG's way of saying that the number 6EH is truly a garbage byte sitting in memory, doing nothing. Executing 6EH as though it were an instruction, however, could cause your machine to do unpredictably peculiar things, up to and including locking up hard.