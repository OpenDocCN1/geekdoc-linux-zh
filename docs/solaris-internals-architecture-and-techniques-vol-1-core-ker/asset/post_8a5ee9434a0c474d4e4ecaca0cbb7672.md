
# Entering Kernel Mode

longer than 8 instructions. This allows branchless inline handlers to be implemented such that the entire handler fits within the trap table slot.

Figure 2.3 shows the UltraSPARC I & II trap table layout.

| Trap Table Contents | Trap Types |
|---|---|
| Hardware Traps | 000...07F |
| Trap Level = 0 | Spill/Fill Traps | 080...0FF |
| | Software Traps | 100...17F |
| | Reserved | 180...1FF |
| Trap Level > 0 | Hardware Traps | 000...07F |
| | Spill/Fill Traps | 080...0FF |
| | Software Traps | 100...17F |
| | Reserved | 180...1FF |

Figure 2.3 UltraSPARC I & II Trap Table Layout

## 2.2.3.5 Software traps

Software traps are initiated by the SPARC trap instruction, Tcc. The opcode for the trap instruction includes a 6-bit software trap number, which indexes into the software portion of the trap table. Software traps are used primarily for system calls in the Solaris kernel.

There are three software traps for system calls: one for native system calls, for 32-bit system calls (when 32-bit applications are run on a 64-bit kernel), and for SunOS 4.x binary compatibility system calls. System calls vector through a common trap by setting the system call number in a global register and issuing a trap instruction. We discuss regular system calls in more detail in “System Calls” on page 44.

There are also ultra-fast system calls implemented as their own trap. These system calls pass their simple arguments back and forth via registers. Because the system calls don't pass arguments on the stack, less of the process state needs to be saved during transition into kernel mode, resulting in a much faster system call implementation. The fast system calls (e.g., get_hrestime) are time-related calls.

Table 2-2 lists UltraSPARC software traps, including ultra-fast system calls.

## Table 2-2 UltraSPARC Software Traps

| Trap Definition | Trap Type Value | Priority |
|---|---|---|
| Trap instruction (SunOS 4.x syscalls) | 100 | 16 |
| Trap instruction (user breakpoints) | 101 | 16 |
| Trap instruction (divide by zero) | 102 | 16 |
| Trap instruction (flush windows) | 103 | 16 |
| Trap instruction (clean windows) | 104 | 16 |
| Trap instruction (do unaligned references) | 106 | 16 |
| Trap instruction (32-bit system call) | 108 | 16 |
| Trap instruction (set trap0) | 109 | 16 |
| Trap instructions (user traps) | 110–123 | 16 |
| Trap instructions (get hrtime) | 124 | 16 |
| Trap instructions (get xrtime) | 125 | 16 |
| Trap instructions (self xcall) | 126 | 16 |
| Trap instructions (get hrestime) | 127 | 16 |
| Trap instructions (trace) | 130-137 | 16 |
| Trap instructions (64-bit system call) | 140 | 16 |

## 2.2.3 A Utility for Trap Analysis

An unbundled tool, trapstat, dynamically monitors trap activity. The tool counts of each type of trap for each processor in the system during an interval specified as the argument. This is currently implemented on UltraSPARC and Intel x86 processor architectures, on Solaris 7 and later releases.

You can download trapstat from the website for this book: http://www.solarisinternals.com. Simply untar the archive and install the driver with the add_drv command.

> Note: trapstat is not supported by Sun. Do not use it on production machines because it loads code into the kernel.

```
# tar xvf trapstat28.tar
-xr-xr-x 0/2 52668 Jan 31 03:57 2000 /usr/bin/trapstat
-rxr-xr-x 0/1 33452 Feb 10 23:17 2000 /usr/bin/sparc7/trapstat
-rwxr-xr-x 0/1 40432 Feb 10 23:16 2000 /usr/bin/sparc9/trapstat
-rw-xr--r 0/1 21225 Sep 11 22:58 1999 /usr/kernel/drv/trapstat
-rw-r--r-- 0/1 188 Aug 31 10:06 1999 /usr/kernel/drv/trapstat.conf
-rw-rw--r-- 0/1 37328 Sep 08 17:28 1999 /usr/kernel/drv/sparc9/trapstat.conf
# add_drv trapstat
```

Once trapstat is installed, use it to analyze the traps taken on each processor.

| vct | name | cpu0 | cpu1 |
|---|---|---|---|
| 24 | cleanwin | 3636 | 4285 |
| 41 | level-1 | 99 | 1 |
| 45 | level-5 | 1 | 0 |
| 46 | level-6 | 60 | 0 |
| 47 | level-7 | 2 | 0 |
| 4a | dlevel-10 | 100 | 0 |
| 4d | dlevel-13 | 31 | 67 |
| 4e | dlevel-14 | 100 | 0 |
| 60 | int-vec | 161 | 90 |
| 64 | tlb-miss | 5129 | 11528 |
| 68 | dtlb-miss | 39130 | 82077 |
| 6c | dtlb-proc | | |
| 84 | spill-1-normal | 1210 | 99 |
| 8c | spill-normal | 136 | 286 |
| 98 | spill-6-normal | 5752 | 20286 |
| a4 | spill-other | 476 | 1116 |
| ac | spill-other | 4782 | 9012 |
| c4 | fill-normal | 1218 | 752 |
| cc | fill-normal | 3725 | 7972 |
| d8 | fill-6-normal | 5576 | 20273 |
| 103 | soft-wins | 31 | 0 |
| 108 | syscall-32 | 2809 | 3813 |
| 124 | gets | 1009 | 2523 |
| 127 | gethtime | 1004 | 477 |
| ttl | | 76401 | 16510 |

The example above shows the traps taken on a two-processor UltraSPARC-based system. The first column shows the trap type, followed by an ASCII description of the trap. The remaining columns are the trap counts for each processor.

We can see that most trap activities in SPARC are register clean, spill, and fill traps—they perform SPARC window management. The level-1 through level 14 and int-vec rows are the interrupt traps. The tlb-miss, dtlb-miss, and dtlb-proc rows are the UltraSPARC memory management traps, which occur each time a TLB miss or protection fault occurs. (“The UltraSPARC I & II” on page 193.) At the bottom of the output we can see the system trap for 32-bit calls and two ultra-fast system calls (gets and gethtime), which each use their own trap.

The SPARC V9 Architecture Manual provides a full reference for the implementation of UltraSPARC traps. We highly recommend this text for specific implementation details on the SPARC V9 processor architecture.

## 2.3 Interrupts

An interrupt is the mechanism that a device uses to signal the kernel that it needs attention and some immediate processing is required on behalf of that device. Solaris services interrupts by context-switching out the current thread running on a processor and executing an interrupt handler for the interrupting device. For example, when a packet is received on a network interface, the network controller initiates an interrupt to begin processing the packet.

### 2.3.1 Interrupt Priorities

Solaris assigns priorities to interrupts to allow overlapping interrupts to have correct precedence; for example, a network interrupt can be configured to have a higher priority than a disk interrupt.

The kernel implements 15 interrupt priority levels: 1 through level 15, where level 15 is the highest priority level. On each processor, the kernel can mask interrupts below a given priority level by setting the processor's interrupt level. Setting the interrupt level blocks all interrupts at the specified level and lower. That is, when the processor is executing a level 9 interrupt handler, it does not receive interrupts at level 9 or below; it handles only higher-priority interrupts.

| High Interrupt Priority Level | | |
|---|---|---|
| 15 | | |
| 14 | | |
| 13 | PIO Serial Interrupts | |
| 12 | | |
| 11 | | |
| 10 | Clock Interrupt | Interrupts at level 10 or below are handled by interrupt threads. Clock interrupts are handled by a specific clock interrupt handler kernel thread. There is one clock interrupt thread systemwide. |
| 9 | | |
| 8 | | |
| 7 | Network Interrupts | |
| 6 | Disk Interrupts | |
| 5 | | |
| 4 | | |
| 3 | | |
| 2 | | |
| Low Interrupt Priority Level | 1 | |

Figure 2.4 Solaris Interrupt Priority Levels

Interrupts that occur with a priority level at or lower than the processor's interrupt level are temporarily ignored. An interrupt will not be acknowledged by a processor until the processor's interrupt level is less than the level of the pending interrupt. More important interrupts have a higher-priority level to give them a better chance to be serviced.

Figure 2.4 illustrates priority levels.

### 2.3.1.1 Interrupts as Threads

Interrupt levels can be used to synchronize access to critical sections used by interrupt handlers. By raising the interrupt level, a handler can ensure exclusive access to data structures for the specific processor that has elevated its priority level. This is in fact what early, uniprocessor implementations of UNIX systems did for synchronization purposes.

Masking out interrupts to ensure exclusive access is expensive; it blocks other interrupt handlers from running for a potentially long time, which could lead to data loss if interrupts are lost because of overrun (An overrun condition is in which the volume of interrupts awaiting service exceeds the system's ability to queue interrupts.) In addition, interrupt handlers using priority levels cannot block, since a deadlock could occur if they are waiting on a resource held by a lower-priority interrupt.

For these reasons, the Solaris kernel implements most interrupts as asynchronously created and dispatched high-priority threads. This implementation allows the kernel to overcome the scaling limitations imposed by interrupt blocking for synchronizing data access and thus provides low-latency interrupt response times.

Interrupts at priority 10 and below are handled by Solaris threads. These interrupt handlers can then block if necessary, using regular synchronization primitives such as mutex locks. Interrupts, however, must be efficient, and it is too expensive to create a new thread each time an interrupt is received. For this reason, each processor maintains a pool of partially initialized interrupt threads, one for each of the lower 9 priority levels plus a systemwide thread for the clock interrupt. When an interrupt is taken, the interrupt uses the interrupt thread's stack, and only if it blocks on a synchronization object is the interrupt completely initialized.
