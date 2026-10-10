```
B,GATE  ,+8,ro  # branch to current address+8
# and raise the privilege level
LDIL  I$ target,r1  # start building a target address
# in r1
B(gateway_generic)  # branch to our new block of code
LDO  R$ target (r1),r1 # complete the target address
(gateway_generic)
MTPS  r0,sr2  # set up sr2 for later use
BE  (sr2,r1)  # branch external to the target
# we have built
DEPI  3,63,2,r31  # set the privilege bits to 3 in
# the stub's return pointer.
```

# Lightweight System Calls

To minimize system overhead cost, some system calls are implemented via simple assembly language routines called lightweight system calls. The lightweight calls simply set or return a value from a process’s or thread’s proc_t, kthread_t, or user_t. They never block, sleep, or have to worry about multiprocessing issues. Lightweight calls include siglock(), sigvector(), getpid(), gettid(), geteuid(), getgid(), getegid(), and umask() for an HP-UX 10.x kernel.

# gateway_page on a Narrow Kernel

On early HP-UX systems, there were fewer system calls, which allowed a single page of system memory to contain a simple redirection routine and up to 253 individual promotion blocks. The gateway_page needed to be accessible from a user thread’s memory map, so it was located at the beginning of quadrant 4, VAS 0 (explicit address of 0x0.C0000000, implicit address of 0xC0000000). This address was hardcoded into the system call stub code for narrow applications and inserted into all SOM executables by the compilers.

As the number of system calls grew, exceeding 253, redirection code at the beginning of the gateway_page was modified so that all system call numbers greater than 253 would be sent to the same address as system call 0. On the kernel side a vector jump table (bysent[ ]) is maintained and indexed by the system call number (passed by the system call stub in r22) to direct the request to the correct target in the kernel.

# Selected Portions of the gateway_page from a 32-Bit HP-UX 11.0 Kernel

Listing 4.1 was created using the adb utility:

```
#  adb -k /stand/vmunix /dev/kmem >> temp
      gateway_page,400?1a
```