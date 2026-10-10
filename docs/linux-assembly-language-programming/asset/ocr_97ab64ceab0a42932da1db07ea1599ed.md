The resources offered by Linux to the programmer are essentially defined by the capabilities of the system calls. One reason for the success of Linux early on was that it was designed to adhere to the POSIX standard for the programmer's system interface. Linux was one of the first operating systems to achieve POSIX compliance. Windows NT is also POSIX-compliant.

# ## 9.6 Privilege Levels

When a system call takes over the processor, it does so because a program needs the kernel to do something which it is unable to do for itself, like read a file or write to the monitor. The program is incapable of these things because the processor itself is blocked from doing them while user code is executing. The difference between kernel code and user code is a difference in *privilege level*. Since the 286, a protection system based on a system of four different privilege levels has been in place. The four levels are

+   - 0 System level privilege, used by the Linux kernel.
+   - 1 Unused in Linux.
+   - 2 Unused in Linux.
+   - 3 User level privilege, used by Linux user programs.

The privilege level of the currently executing code is called the *current privilege level*. It is stored in a two-bit register called the CPL register.

# ### 9.6.1 The CPL Register

The CPL register is one of the most important registers on the machine. Level 0 has the most privilege. Changing the CPL value to 0 is like disengaging the safety catch on the processor. It takes place every time a system call is executed. It is a more drastic step than becoming superuser. From the standpoint of CPL-based privilege, the superuser is just another user. But when the CPL is 0, the processor can do things that *no* user can do. For example, it can modify the page tables or change the interrupt descriptor table.

Of course, given that `root` is the owner of the disk image of the kernel, the file `vmlinux` in the root directory, `root` can do whatever it wants indirectly by changing this file. `root` can also modify kernel code which is stored in modules. But these changes will only take effect the next time the system is booted or a kernel module is loaded.

# ### 9.6.2 Privileged Instructions

The `LIDT` instruction changes the address stored in the IDT register. This is the address that the processor goes to when it receives an interrupt. This instruction has the effect of changing from one interrupt table to another one. If used by a user, it could be used to take control of all interrupts by sending the processor to a private table for the handling of all interrupts. It is a good example of what is called a *privileged instruction*. The processor will not execute a privileged instruction unless the CPL = 0. If this instruction is included in code which is executing while the CPL > 0, for example, in user code where the CPL = 3, it causes an exception called a *general protection error*. See Table 9.4.

The `MOV` mnemonic names an instruction that can be used to access the control registers. The command

```
MOV reg, reg
```

where one `reg` is a control register and the other is a 32-bit general register, can be used to load a value into CR3, for example. CR3 holds the address of the page table table where address translation begins. Loading a new value into CR3 has the effect of changing from one set of page tables to another. If this could be done by a user the user could take control of *physical memory*. `MOV` used with control registers is another good