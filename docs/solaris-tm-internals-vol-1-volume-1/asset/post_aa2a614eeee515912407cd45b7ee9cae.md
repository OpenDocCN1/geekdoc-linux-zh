
## 9.5 Kernel Processor Control and Processor Sets

Every operating system requires intimate knowledge of the hardware processors it supports and has low-level kernel code to manage things like processor state, trap and interrupt handling, clock tick processing, thread context switching, memory management, stack management, etc. The Solaris kernel extends the notion of processor control considerably beyond traditional implementations. The current model in the Solaris kernel was driven by several requirements of two goals:

- **Multiprocessor system efficiency.** Sun leads the industry in building scalable multiprocessor server systems based on the Symmetric Memory Processor (SMP) architecture. This architecture is defined as some number of processors that share a single image of the operating system, the system’s physical address space (physical memory and I/O space), and the kernel’s virtual address space. Building an operating system that manages processor resources effectively and efficiently is key to system scalability and management.
- **Resource management and control.** The ability to manage the hardware resources of a system effectively, such that applications or groups of users can be guaranteed some percentage of available processor resources, has become a mainstream requirement in all facets of computing. Other control mechanisms such as dynamically taking processors offline without affecting the entire system, bringing processors online, redirecting interrupts, and even powering processors down are also features that are much in demand.

The Solaris kernel delivers on these requirements with a kernel implementation built around per-processor data structures and kernel code functions for processor management and integration into related areas of the operating system, primarily the kernel threads scheduler, or dispatcher.

Every processor on a Solaris system has a corresponding data structure, the cpu structure, which maintains various bits of information, such as the state of the processor, and links to resources used by the processor, such as its dispatch queues, an idle thread, and interrupt threads. The cpu structure members can be categorized by function.

- **General information** — The CPU identification number, a sequential ID number, and state flags.
- **Kernel thread pointers** — Pointers to the currently executing kernel thread, an idle kernel thread, and a pause kernel thread; a pointer to the current LWP.
- **CPU structure linked lists** — A CPU appears on one or more linked lists maintained in the kernel; a list of existing (installed and configured) CPUs, a list of online CPUs, and a list of other CPUs in the same processor set; a pointer to a cpu-part structure (CPU partition) for processor set support.
- **Scheduling variables** — The per-processor dispatch queue (queue of runnable kernel threads), scheduling flags to manage thread preemption, and per-kernel thread scheduling information.
- **Interrupt information** — The CPU's interrupt stack, a pointer to a linked list of interrupt threads, a flag to indicate the CPU is running on the interrupt stack, and interrupt-level information.
- **Statistics** — Statistical data, mostly in the form of counters, on CPU activity (used by sar(1M), vmstat(1M), and mpstat(1M)).
- **Configuration and control data** — Processor information such as the CPU type, Floating Point Unit (FPU) information, and clock speed; control for state changes and checkpoint/resume support.
- **Architecture-specific data** — Processor architecture-specific control and information, such as fine-grained clock tick data, architecture-specific interrupt data, and processor control block for saving hardware state (general registers, floating-point registers, etc.).

The structure, defined in `/usr/include/sys/cpuvar.h`, is illustrated in Figure 9.17.

![](img/220ae4af07df2fe8e5be69d27f885d1b_462_0.png)

**Figure 9.17 CPU Structure and Major Links**

Most of the fields in the CPU structure are machine independent and thus apply to all platforms supported by the Solaris environment. As we indicated earlier, the data that is architecture specific is referenced through the `cpu_m` field in the structure, which contains the machine-dependent data and links to the processor-specific processor control block (PCB). The `cpu_stat` field is an embedded data structure that combines most of the kernel-maintained counters defined in `/usr/include/sys/sysinfo.h`. Per-processor statistical information is maintained and reported by utilities like mpstat(1M). Other bundled tools, vmstat(1M) and sar(1M), provide systemwide statistics by summing the per-processor data.

The linked lists of CPU structures are all doubly linked, with a forward and backward pointer. The diagram in Figure 9.17 shows only the forward pointer names (e.g., `cpu_next_xxx`), but every forward link also has a corresponding `cpu_prev_xxx` back pointer. The primary linked list is all configured processors, linked by `cpu_next`/`cpu_prev`. All online processors are linked by `cpu_next_onln`/`cpu_prev_onln`. A processor taken offline by `psradm(1M)` command or `p_online(2)` system call is removed from the online linked list and taken out of the dispatcher—kernel threads will not be placed on an offline processor’s dispatch queues. Offline processors can still field interrupts.

### 9.5.1 Processor Control

The system creates several kernel threads that serve a specific purpose for CPU control or general operating system activity. The interrupt threads are designed to facilitate fast switching to and from an interrupt handler by having a thread ready to execute interrupt handling code. The linked list is created at boot time, one thread for each interrupt level—10 on the Ultra Enterprise Server systems. (There are actually 15 interrupt levels, but levels above 10 do not require an interrupt thread.) The idle thread is executed if there are no runnable threads on any of the dispatch queues when the scheduler runs. The idle thread essentially loops, calling the dispatcher function to examine the queues, looking for the highest (best) priority runnable thread. The pause thread exists as part of the processor control facilities and keeps the CPU in a safe place in the interim between state changes (e.g., online to offline).

A CPU in Solaris can be in one of several possible states, as defined by the bits set in the `cpu_flags` field.

- **CPU_RUNNING.** The CPU is running, able to execute kernel threads, handle interrupts, etc.
- **CPU_READY.** The CPU will take cross-calls and directed interrupts.
- **CPU_QUIESCED.** The CPU is not running kernel threads or interrupt threads.
- **CPU_EXISTS.** All installed CPUs when the system initializes (boots) will minimally be in the EXISTS state.
- **CPU_ENABLE.** The CPU is enabled to take interrupts, but it is not part of the dispatcher’s pool of online CPUs to schedule kernel threads. With this flag off, the CPU may still take directed interrupts and cross-calls, but not interrupts that can be directed to another CPU.
- **CPU_OFFLINE.** The processor was taken offline by `psradm(1M)` or `p_online(2)` and is no longer scheduling kernel threads. The CPU will still take interrupts. (That’s the difference between the offline state and quiesced state—a CPU in the quiesced state will not take interrupts.) A CPU with bound threads cannot be taken offline.
- **CPU_POWEROFF.** (Solaris 2.6 and Solaris 7 only) The CPU has been powered off.

You can examine the CPU structures on a running system by using an available adb macro, cpu. (adb macros can be found in the `/usr/lib/adb` directory.) The kernel maintains the address of the first CPU structure in the linked list in a kernel variable called `cpu_list`.

```text
# adb -k
physmem 3b5f
cpu_list/k
cpu_list:
cpu_list:        1041ad20
1041ad20$<cpu

cpu0:
cpu0:            id                 seqid                 flags
                 0                  0                     1b
cpu0+0x10:       thread             idle_thread            pause_thread
                 30000ab8fe0        2a10001fd40            2a1000fd40
                 lwp                parent                part
cpu0+0x28:       1000007000         0                      1041be88
                 next               prev                   next_onln
cpu0+0x48:       300003d2010        300003d2010            300003d2010
cpu0+0x60:       prev_onln          next_panic             prev_part
                 300003d2010        300003d2010            300003d2010
                 disp
cpu0+0x78:       lock               npri                   queue
                 0                   170                    3000048a000
cpu0+0x88:       limit              actmap                 maxnpri
                 3000048aff0        300004a840             -1
cpu0+0x9a:       max_unb_pri        n runnable
                 -1                  0

cpu0+0xa8:       rqhru n            kprunru                chosen_level
                 0                   0                      -1
cpu0+0xb0:       disp_thread        thread_lock            last_switch
                 30000ab8fe0        0                      12e9f54
cpu0+0xc8:       intr_stack         on_intr                intr_thread
                 2a10001bf50        0                      300007dd40
cpu0+0xe0:       intr_actv          base_spl               profile_cyclic_id
                 0                  0                      0
cpu0+0x278:      0 profile_pc       profile_pil            profile_when
                 syscall_trap+0x28  0                      0
                 profile_late       cyc_cpu
                 53                 30000067c8
```

To look at structures for the remaining processors, feed the next value into the adb cpu macro.

Note the flags field, which is the `cpu_flags` member. This example represents the state after bootstrap of a CPU that has not had its state altered explicitly. Following initialization, the set `cpu_flags` bits are CPU_RUNNING,
