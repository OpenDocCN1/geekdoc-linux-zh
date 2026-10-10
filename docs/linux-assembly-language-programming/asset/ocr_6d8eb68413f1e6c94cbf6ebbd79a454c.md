of a user, the user could take control of physical memory, but deal with control registers is another good example of a privileged instruction.

# 9.6.3 Stack Problems

Since the ISR code that the interrupt is jumping to may well use the stack, it is important that the stack not be subject to write access by the user. Even though user code will not function again until the ISR exits, there can still be trouble. For example, suppose that the system call read( ) is being executed. read( ) transfers data from a file to user memory. One of the parameters to this call is the address of some memory that the user has permission to write on. In executing the call, the system will store file data at that address. If the stack being used by the system is the user's stack, then the user has permission to write on it. The user may then supply the stack address as parameter to read( ) and the system will then mess up the stack it is using at the very time it is using it. This would cause a crash.

User code writes where it shouldn't, usually by mistake and not out of malice. But it happens a lot. That's why the Segmentation Fault error message is so gallingly familiar. Code for system calls like read( ) needs to use its own stack. There is a different stack for each value of the CPL. Changing stacks is taken care of by the hardware! Each stack has its own stack pointer. These four stack pointers are stored in a memory area called the Task State Segment.

The layout of a gate is built into the x86 processor. Figure 9-7 shows the most important fields in a gate. These fields contain two items that pertain to this

![](bbox=[0.06, 0.39, 0.94, 0.49])

discussion. They are

+   - A four-bit type value which is stored in bits 40–43.
+   
+   - The address of the ISR. This 32-bit address is located in bits 48–63 and bits 0–15 of the table entry.

Interrupt gates are used for hardware interrupts. A trap gate is used for the INT 80H system call interrupt.

# 9.7 Control Transfer

Based on the two items of information gleaned from the gate, the actions discussed in sections 9.7.1 through 9.7.4 are taken.

# 9.7.1 Clear the Interrupt Enable Flag?

When the x86 loads a descriptor table entry in response to an interrupt, the four-bit type value is checked to see if the interrupt enable flag should be cleared. If the type value is 14, the interrupt enable flag is cleared just as it is on the 8086. Twelve of the 16 possible four-bit values are defined.

Table 9.6. Interrupt Gates vs. Trap Gates

| Type Value | Gate Type | Clear IE Flag |
| :--- | :--- | :--- |
| 14 | Interrupt Gate | Yes |
| 15 | Trap Gate | No |

# 9.7.2 Store 0 into the CPL