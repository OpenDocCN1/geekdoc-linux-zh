A deeper look into a process reveals that it in fact consists of the following three entities:

+   1. The address space
+   2. The CPU state
+   3. The process control block

The address space of the process is dictated by the main memory image of the process, as discussed in Chapter 10, Section 10.5.1. The values of the CPU registers at any given time, including the value of the program counter, comprise the CPU state of the process. We describe the enhanced version of the main memory image of a process, the address space of a process, and the process control block (PCB) of a process in the next subsection.

# 19.2.2 Process Control Block

The PCB is a kernel data structure that keeps track of the run-time attributes of the process. In UNIX, the PCB of a process consists of two parts: the proc structure and the u area. Whereas the proc structure contains the scheduling-related information of a process, the u area contains information about signal handling, resource allocation, and a reference to the proc structure. The proc structure of a process always remains in the main memory regardless of the state of the process. However, the u area is in the main memory only when the process is in the running state.

The proc structure contains the PID and PPID, its priority, scheduling and waiting queues, information about memory management (paging and segmentation), the process state, and the signal-handling mask. The u area contains a pointer to the proc structure, the CPU state (i.e., context) of a blocked process, the UID and GID, the current directory, CPU usage of the process, the terminal the process is attached to, signal-handling information, and the PPFDT.

A process may not access its PCB directly; the kernel updates the proc structure fields of a process as and when needed. For example, the kernel code updates the scheduling priority field in the PCB of a process when the process priority changes. Although a part of a process image, the u area is only accessible to a process through the kernel code that executes on behalf of the process, such as the code for a system call.

# 19.2.3 Process Memory Image (Process Address Space)

We discussed the memory image of a UNIX process in detail in Chapter 10. As stated earlier, the process memory image, also known as the process image, consists of several sections, as shown in Figure 10.6. Figure 19.1 shows the complete version of the process image, including the u area at the top of the image. The memory image of a process delineates the main memory region(s) that a process may access legally, known as the process address space.

Some of the regions of the process image come into being only while the process remains in the system (running or waiting for an event); other regions are an integral part of the process image, whether it is a process in the main memory or an executable image on