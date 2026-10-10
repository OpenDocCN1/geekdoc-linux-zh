file system forwards requests to the relevant modules of the I / O subsystem, and those - directly to the peripheral devices. In addition, the file subsystem controls file access rights, which largely determine the privileges of the user on the system.

The I / O subsystem performs file system requests by interacting with device drivers. In UNIX, two types of devices: character (eg, printer) and block (eg, hard disk). The main difference between them is that the block device allows direct access. To increase the productivity of block devices using the buffer cache - plot memory which stores data last scanned from the disc. Subsequent accesses to these data can be retrieved from the cache.

# ## Linux Architecture

There are three main parts to Linux :

+   - Core, which implements the basic functions of the OS (process management, input-output, memory, etc.)
+   - System libraries that define a standard set of functions for use in applications (performing such functions does not require a transition to privileged mode)
+   - System utilities (applications that perform specialized tasks)

# ## The Purpose Of The Linux Kernel And Its Features

Linux implements a monolithic kernel technology. All kernel data and data structures are in the same address space. There are several functional components in the kernel.

+   - Process Scheduler - Responsible for the implementation of multitasking in the system (interrupt processing, timer operation, creation and completion of processes, context switching)