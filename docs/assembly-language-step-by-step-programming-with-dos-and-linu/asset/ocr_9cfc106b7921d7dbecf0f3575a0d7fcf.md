To find the way home, the IRET instruction need only fetch the address at the top of the stack...

| Free Memory |
|---| 
| MYPROG.EXE Return Address Stack Code |
| INT 21H |
| DOS Dispatcher |
| IRET |
| Vector 21 Vector Table |

...and jump to that address, Execution then resumes at the instruction just after the INT 21 that started the journey!

= movement of addresses
= flow of execution

**Figure 8.5** Returning home from an interrupt.

“combination” instruction that pops the return address off the stack and then jumps to the address. The instruction is IRET (for Interrupt Return), and it completes this complex but reliable system of jumping to an address when you really don’t know the address. The trick, once again, knowing where the address can reliably be found. (There’s