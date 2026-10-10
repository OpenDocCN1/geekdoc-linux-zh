Linux maintains a count of the interrupt requests which come in on the IRQ lines. To see this count, you may use the command

```
```python
   linuxbox> cat /proc/interrupts
```
```

The output of this command should be compared with Table 9.3.

# ### 9.4 Internal and Software Interrupts

Interrupts which do not arise as the result of an external signal on an interrupt pin also exist.

# #### 9.4.1 Exceptions

Suppose that the fetch-execute cycle encounters the machine code F0FH. This machine code is not defined. Suppose a MOV instruction attempts to access a memory address to which the operating system has not given permission. Suppose that the DIV command produces a quotient which is too big for the destination register. Suppose that the stack overflows. These are situations where the designers of the x86 preferred to delegate to the operating system the decision as to what action should be taken. In fact, they forced the operating system to take over at these points by assigning interrupt numbers to these *exceptions*. These interrupt numbers are built into the x86 processors. Exceptions do not use interrupt acknowledge bus cycles. But they must be handled by numbered ISRs, just as external interrupts are.

# Table 9.3. ISA Interrupt Routings

| IRQ | Allocation | Interrupt Number |
| --- | --- | --- |
| IRQ0 | System Timer | 08H |
| IRQ1 | Keyboard | 09H |
|  |  |  |
| IRQ3 | Serial Port #2 | 0BH |
| IRQ4 | Serial Port #1 | 0CH |
| IRQ5 | Parallel Port #2 | 0DH |
| IRQ6 | Floppy Controller | 0EH |
| IRQ7 | Parallel Port #1 | 0FH |
| IRQ8 | Real Time Clock | 70H |
| IRQ9 | available | 71H |
| IRQ10 | available | 72H |
| IRQ 11 | available | 73H |
| IRQ 12 | Mouse | 74H |
| IRQ13 | 87 ERROR line | 75H |
| IRQ 14 | Hard Drive Controller | 76H |
| IRQ15 | available | 77H |

Table 9.4 lists the exceptions which are built into the x86 processors. Note that some of these interrupt numbers are the same as the interrupt numbers reported by an ISA interrupt controller. When interrupts are shared like this, the ISR is stuck with the responsibility for distinguishing which situation has caused the interrupt.

# #### 9.4.2 Software Interrupts

In order to make the interrupt service routines accessible to programmers, the INT instruction was added to the instruction set. The syntax is simply

```
```
INT imm
```
```