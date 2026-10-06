
## 22 CHAPTER 1 Early Intel® Architecture

To accommodate this, the segment register format and behavior in protected mode is completely different from the segment register format and behavior in real mode.

Remember that originally the segment registers simply contained a base address that was shifted and the offset to produce a larger address size. In this new model, the segment registers needed more room for the accounting required to support these new features. Therefore, in protected mode, only now didn't reference the base address of the segment, but instead pointed to a descriptor entry in a table of segment descriptors. Each 8-byte entry in this table describes the 24-bit base address, 16-bit size, and 8 bits for the privilege and access information, which is used for marking segments as read only, executable, and so on. The remaining 16 bits store the segment selector, when loaded into the 16-bit segment register effectively load the descriptor. To improve performance, by avoiding the need to touch each time a segment operation must be checked, the other 48 bits of the segment descriptor are cached in a hidden register when the segment selector is loaded.

 order to make segmentation useful for both the operating system and user applications while enforcing memory protections, the segment descriptor table (GDT) is a table of segment descriptors that the operating system, privilege level 0, controls, while the local descriptor (LDT) is controlled by the user application. Registers, the GDT and LDT, exist for storing the base address of these tables. The global and local descriptors are loaded and stored with the LGDT and SGDT, and LDT and SLDT instructions. Each segment selector has a special bit indicating whether the descriptor is located in the local or global table.

Each segment descriptor also had a present bit, indicating whether the corresponding segment was currently loaded into memory. If the segment descriptor was not set, the bit in the descriptor was, the user program would be paused and an exception would be raised, giving the operating system a chance to load the relevant segment from memory from disk. Once the segment had loaded, the user program would be resumed. All of this occurred transparently to the user program, and thus provided an early form of hardware supported virtual swapping. With swapping, more virtual memory could be allocated by the operating system than was physically allocated on the computer.

### 1.3.3 TASK CONTROL

Since the processor is only capable of running one application at a time, the job of a multitasking operating system is to provide the illusion that the processor can run multiple tasks at once. Whereas in a single-tasking operating system each job runs from start to completion before next job, a multitasking operating system divides the processor time across each of the required jobs. This switching has to occur quickly and smoothly enough that it is transparent to the user applications, and appears that the processor is running all of the tasks concurrently.

## 1.4 Intel® 80386 and 80387

The action of switching the processor from one process to running a different process is referred to as a context switch. In order to perform a context switch, the operating system must keep track of the full execution state of the process, including the contents of the registers, and for each executing task. In a context switch, the process which was running and the contents of the execution state are saved into storage, while the execution state of the new process to run is loaded from storage into the processor.

The process of determining which process should be run and for how long is referred to as process scheduling. Process scheduling is a well researched problem in computer science that attempts to address many concerns, such as fairness in scheduling or balancing time with throughput, for many different types of situations involving different numbers of processes with different performance requirements. As such, process scheduling is a fairly large field, which will be discussed in detail within this book. At the time of this writing, the process scheduling for Linux revolves around scheduling tasks to complement power-saving techniques. For a good introduction to the fundamental concepts and algorithms, the author recommends Modern Operating Systems by Andrew Tanenbaum.

The 80286 introduced a new feature that allowed for context switches to be handled automatically in hardware. This was facilitated by a special, task segment. Within the task segment, all of the execution state of a process is preserved. By issuing a JMP, CALL instruction, or returning from an interrupt, the destination is the TSS' descriptor, a context switch automatically occurs. The execution state of the currently executing process is automatically copied into the relevant section of the TSS. Once this is complete, the new execution, of the process switched to, is automatically loaded into the processor, and the execution of the new process can continue from where it had been previously paused.

Despite full support for context switches in hardware, Linux performs all of its context switches manually with software. This has been done for performance reasons, because the hardware context loads and validates all of the execution state, whereas Linux has historically performed some of the loads lazily and optimized some loads based on what actually needs to be restored.

## 1.4 INTEL® 80386 AND 80387

After the 80286, the 80386, shown in Figure 1.4, was introduced in 1985, and was continually produced by Intel, by popular demand, until September 2007. The 80386 was the first 32-bit processor in the x86 family, and also expanded many of the fundamental concepts introduced in the 80286. Perhaps even more importantly, since this book focuses on Linux, the 80386 was the first processor to ran Linux. In fact,

![](img/33fad1fa149d4f0cdd55ff2565970ab2_41_0.png)

FIGURE 1.4
Intel® 80386 (Lanzet, 2008).

80386 support exists in the kernel until it was removed in 2012 (Molnar, 2012). To quote the original Usenet post by Linus Torvalds describing the Linux project:

> “I’m doing a (free) operating system (just a hobby, won’t be big and professional like gnu) for 386/486 AT clones... It uses every conceivable feature of the 386 I could find, as it was also a project to teach me about the 386. (Torvalds, 1991)”

Whereas the 80286 introduced the real and protected processor modes, the 80386 introduced an additional mode. This mode, Virtual 8086 mode, was designed to address the fact that the 80286 did not allow returning to real mode from protected mode by side. Virtual 8086 mode is a special mode designed to be entered from protected mode. This allows for the processor to execute 8086, and the 80286 did not allow returning to real mode from protected mode by side.

### 1.4.1 Virtual 8086 mode

Virtual 8086 mode is a special mode designed to be entered from protected mode. This allows for the processor to execute 8086, and the 80286 did not allow returning to real mode from protected mode by side.

### 1.4.2 32-bit mode

After the 80286 introduced the real and protected processor modes, the 80386 introduced an additional mode. This mode, Virtual 8086 mode, was designed to address the fact that the 80286 did not allow returning to real mode from protected mode by side. Virtual 8086 mode is a special mode designed to be entered from protected mode. This allows for the processor to execute 8086, and the 80286 did not allow returning to real mode from protected mode by side.

### 1.4.3 32-bit registers and 80387

After the 80286 introduced the real and protected processor modes, the 80386 introduced an additional mode. This mode, Virtual 8086 mode, was designed to address the fact that the 80286 did not allow returning to real mode from protected mode by side. Virtual 8086 mode is a special mode designed to be entered from protected mode. This allows for the processor to execute 8086, and the 80286 did not allow returning to real mode from protected mode by side.
