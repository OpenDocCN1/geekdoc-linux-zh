
## Step 2
It fetches the address of the correct interrupt service routine from the interrupt table in memory.

## Step 3
It transfers control to the interrupt service routine.

Once the interrupt has been handled, it resumes processing where it left off. Interrupt service routines are somewhat like ordinary subroutines. One important difference is that they are called on signal from the hardware.

### The Interrupt Acknowledge Bus Cycle
Since the x86 receives its general interrupts all via one pin, it cannot tell from a single "knock on the door" which I/O device is signaling for attention. As shown in Figure 9-2, the interrupt controller circuit is connected to the data bus just like memory and I/O. To get the required identification from the interrupt controller, the processor performs a read, which is analogous to a memory or an I/O read. It is called the interrupt acknowledge bus cycle. Just as the processor uses the M/IO# pin to indicate whether it is commanding a memory or an I/O read, it uses the D/C# pin to distinguish an I/O controller read from the memory and I/O read cycles. D is for data and C is for code. The complete list of the bus cycles defined by the D/C#, M/IO#, and W/R# pins is given in Table 9.1.

When the processor receives an interrupt, it initiates an interrupt acknowledge bus cycle. Only the interrupt controller may respond to an interrupt acknowledge bus cycle. It responds by depositing a one-byte number on the bottom eight bits of the data bus. This number is called the interrupt number. It is not the same as an IRQ number. The processor reads the interrupt number off the data bus.

#### Table 9.1. 486 Bus Cycle Definition Pins
| | D/C# | M/IO# | W/R# |
| :--- | :---: | :---: | :---: |
| Interrupt Acknowledge | 0 | 0 | 0 |
| Halt/Special Cycle | 0 | 0 | 1 |
| Code Read | 0 | 1 | 0 |
| reserved | 0 | 1 | 1 |
| I/O Read | 1 | 0 | 0 |
| I/O Write | 1 | 0 | 1 |
| Memory Read | 1 | 1 | 0 |
| Memory Write | 1 | 1 | 1 |

### ISR Address Fetching
The processor then takes this number and uses it as an index into a table called the Interrupt Descriptor Table. This table contains the addresses of the Interrupt Service Routines. See Figure 9-3. Since the interrupt number is an eight-bit number, the valid interrupt numbers range from 0 to 255.

Figure 9-3. Interrupt Descriptor Table, b = IDT register
| Address | Gate # |
| :--- | :--- |
| b | 0 |
| b + 8 | 1 |
| b + 16 | 2 |
| b + 24 | 3 |
| b + 32 | 4 |
| b + 40 | 5 |
| ... | ... |
| b + 2040 | 255 |

It is the responsibility of the operating system to create this table. It is also responsible for loading into memory the interrupt service routines whose addresses are listed in this table. These two jobs are done as a part of the system boot. If they have not been done, the system will be unable to respond to interrupts. When Edlinas displays a "Processor halted" message, it is usually because it is trying to respond to an interrupt and no interrupt table has been built.

## The Interrupt Descriptor Table
The x86 has a dedicated register which stores the address of the interrupt descriptor table, or IDT. It is called the IDT register. There are special commands for accessing this register. The command

```
LIDT mem
```

loads the register. The command

```
SIDT mem
```

stores the contents of this register. The LIDT command is used in setting up the operating system at boot time. Once an interrupt descriptor table has been created, the LIDT command can point the processor to it. In responding to an interrupt, the x86 uses the fact that each table entry occupies eight bytes of space. Consequently, if $b$ is the address stored in the IDT register, then in response to the interrupt numbered $n$, the x86 fetches the eight bytes starting at the address $b + 8 \times n$. These eight-byte entries are called gates.

## ISR Execution
Once the address of the interrupt service routine is obtained, it is treated almost like a CALL instruction treats an address. Before jumping to a target address a CALL instruction pushes the next address after its own address onto the stack. This means that the called routine may return to the instruction following the CALL by reading its address off the stack. Since an interrupt service routine also needs to execute a return the address of the instruction which would otherwise have been executed, had the interrupt not arrived, is pushed onto the stack before the ISR is executed. But in the case of an interrupt, the flags register is pushed also. The interrupt service routine does whatever business is demanded by the interrupt. An interrupt service routine should end with an IRET instruction which is like a RET instruction except that it pops the flags register.

The flags register is a 32-bit register named EFLAGS, which contains all the flags. It is an extension of the 16-bit FLAGS register. Table 9.2 shows the flags in the EFLAGS register on a 486.

The reason for the x86's special flag behavior when responding to interrupts has to do with the problem of interrupt arbitration.

## 9.2.2 Interrupting an Interrupt
What happens when an interrupt occurs while an ISR is already executing? Can one device interrupt another's ISR? Imagine two devices, each refusing to be preempted by the other's ISR. The processor would get bounced back and forth from one ISR to the other until the accumulation of pending return addresses on the stack overflowed and caused the system to crash.

#### Table 9.2. EFLAGS Register
| Bits | Label | Full Name |
| :--- | :--- | :--- |
| 18 | AC | Alignment Check |
| 17 | VM | Virtual 8086 Mode |
| 16 | RF | Restart Flag |
| 14 | NT | Nested Task |
| 13-12 | IOP L | I/O Privilege Level |
| 11 | OF | Overflow Flag |
| 10 | DF | Direction Flag |
| 9 | IF | Interrupt Enable Flag |
| 8 | TF | Trap Flag |
| 7 | SF | Sign Flag |
| 6 | ZF | Zero Flag |
| 4 | AF | ASCII Overflow Flag |
| 2 | PF | Parity Flag |
| 0 | CF | Carry Flag |

### The Interrupt Enable Flag
The design of the 8086 allows for a very simple way to avoid this situation. The idea would be to enforce a strict "one-at-a-time" interrupt policy. It would work by automatically blocking interrupt signals while an ISR is running, and then unblocking them when it is finished. One of the flags on the x86 processor is called the interrupt enable flag. When this flag is cleared, all signals on the general-purpose interrupt pin are ignored. When an 8086 enters an ISR, this flag is automatically cleared. That is why the processor pushes the flags register onto the stack just before entering an ISR. It allows the interrupt enable flag to be restored to its original state when the ISR is done. When the interrupt enable flag is set, interrupts are handled normally.

The one-at-a-time interrupt policy would make life easy for the interrupt controller. The controller could process an incoming interrupt by just passing it along to the processor until it was acknowledged. As soon as the interrupt acknowledge was received, the controller could wash its hands of that interrupt because the processor could be counted upon to work on it nonstop until it was done.

Although the one-at-a-time policy is very easy to implement on an x86 processor, standard PCs do not use it. The problem with it is that interrupts that need a quick response can be kept waiting. If a serial port is getting ready to start trashing data because its buffer is full, then it should not be made to wait while a floppy drive looks for a good sector. A processor with a one-at-a-time interrupt policy can be like a household with a single, occupied bathroom. Unlike the situation with bathrooms, however, interrupting an ISR is not necessarily rude. It sometimes makes good sense to interrupt an ISR.
