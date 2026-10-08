# STARTING THE KERNEL 65

cards are set to the same interrupt or I/O port (either via jumpers or software configuration). The automatic hardware detection can be influenced by means of command line parameters for the kernel. Also consult the up-to-date README files in the kernel sources.

Now, the processor is switched from privileged (or kernel) mode into privileged(or user) mode; from now on, the first UNIX process runs with process number 0). This process is in principle the same as all other UNIX processes, but it runs only if no other process is active. Process 0 is the idle process, which in case of non-use of the processor 100% of the system resources.

Process 1 is started from process 0 by means of the system call fork(). This process in turn initiates the further initialization of the system. Here, the hardware is initialized, the root partition is mounted, and the init program is executed. In UNIX, init is often called the parent of all processes, for whichUX is not entirely correct; here, by right, would be the idle process with the number 0. One further process is started which takes care of regular updates of the internal information about the file system on the hard disk the behaviour of this process can be influenced by means of the bdflush program.

According to the file system hierarchy standard (FHS version 2.0), the init process should be located in /sbin/init. The actual search order established in linux/unix/main.c is, however, /etc/init, /bin/, and /sbin/init. If init is not found, an attempt is made to start /etc/rc or /bin/sh to allow the repair of a 'disordered' system. With current kernel versions it is possible to use the command line parameter INIT=/bin/sh to start a shell instead of init.

To conclude the initialization, the kernel reports its version number and creation date. First, one of the three init processes normally used under LINUX is started. This connects the system start-up from the point of view of the kernel. However, the system can still not be used at this point because no login can take place and no background processes (daemons) have been started.

Now the kernel may start more processes or 'kernel threads' to carry housekeeping, such as flushing dirty buffers to disk, or memory management.

+   4. The privileged mode should not be confused with the protected mode.
5. This fork works in a different way as process 0 has a special role: it works with the same memory area as process 1, in particular with the same stack. Therefore, process 0 only carries out operations that do not use the stack. Quoted from Beck, M. et al. (1997).