The next step in the processing of an interrupt is that 0 is loaded into the CPL. Confidence in the safety of this step must be based on confidence in the code that is being jumped to.

The original value of the CPL is restored when the `IRET` instruction executes.

The mechanism behind the CPL store and restore is discussed in chapter 13.

# 9.7.3 Change Stacks

The ESP used by the kernel is waiting in the task state segment. The ESP corresponding to CPL = 0 is loaded from there into ESP when 0 is loaded into the CPL. The current ESP is not stored in the task state segment. It is pushed onto the new stack.

The fact that the task state segment is not changed when 0 is stored into the CPL is sometimes what is meant by saying that the kernel is executing “within” a task or “in behalf of” a task. In other words, there is no task switch involved. The same task is still running.

# 9.7.4 Jump to the ISR

To do the jump, the return address of the next instruction is pushed onto the new stack. The new EIP is then loaded with the 32-bit address from the gate.

When these four steps have been completed, control has been transferred to kernel code, which runs at CPL = 0. The resources of the processor, which are accessible from this level of privilege, include all the data structures vital to the functioning of the operating system as well as the hardware and the memory.

When the ISR is concluded, then with one exception, control is returned to the user code. Both the old stack and the CPL are restored. The exception is in the case of the timer interrupt.

# 9.8 Scheduling

In Table 9.3 we see that the maskable interrupt with the highest priority is the timer interrupt. The ISR for this interrupt keeps track of time used by all processes. In particular, it sets a flag called `need_resched` when a process is out of time. When Linux does a return from any interrupt, the timer interrupt included, it checks this flag, and calls the `schedule()` if `need_resched` is set. The `schedule()` system call is the *scheduler*. It is the central program in the operating system. It determines which process gets to run next. When necessary, it initiates a task switch.

So the ultimate computing resource, processor time, also falls under the control of the CPL-based protection system.

# Further Reading

> ISA System Architecture, TomShanley and DonAnderson, Addison-Wesley: 1995.

> Interrupt-Driven PC System Design, JosephMcGivern, Annabooks: 1998.

# Chapter 10, BIT MANIPULATIONS

+   10.1 Bitwise Logic Operations
+   10.2 The AND, OR, NOT, and XOR Commands
+   10.3 Bit Setting and Testing
+   10.4 Shift Instructions