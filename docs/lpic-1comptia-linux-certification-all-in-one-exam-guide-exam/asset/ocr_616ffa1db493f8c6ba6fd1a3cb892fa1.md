In the preceding paragraph, I put the term *concurrently* in quotes because most CPUs can't truly run multiple processes at the same time. Instead, the Linux operating system quickly switches between the various processes running on the CPU, making it appear as if the CPU is working on multiple processes concurrently. However, the CPU actually only executes a single process at a time. All other processes currently “running” wait in the background for their turn. The operating system maintains a schedule that determines when each process is allowed access to the CPU. This is called **multitasking**. Because the switching between processes happens so fast, it appears, to you and me at least, that the CPU is executing multiple processes at the same time.

> **NOTE**  Multicore CPUs do actually execute more than one process at a time. Because there are two cores within the CPU, one core can execute one process while the other core works on another. Hyperthreading CPUs can also process more than one process at a time.

The Linux operating system uses several types of processes. Let’s review those next.

# ## Types of Processes

Not all processes on your Linux system are the same. Some processes are created by the end user when he or she executes a command from the shell prompt or through the X graphical interface. These processes are called **user processes**. User processes are usually associated with some kind of end-user program running on the system.

For example, if you run the OpenOffice.org suite (**oofromtemplate**) from the shell prompt, a user process for the OpenOffice.org program is created. This is shown in Figure 13-1.

The key point to remember about user processes is that they are called from within a shell and are associated with that shell session.

However, not all processes running on your system are user processes. In fact, most processes executing on a given Linux system will probably be of a different type called *system processes* or **daemons**. Unlike a user process, a system process (usually) does not provide an application or an interface for an end user to use. Instead, they are used to provide system services, such as a Web server, an FTP server, a file service such as Samba, a print service such as CUPS, a logging service, and so on. These processes run in the background and usually don’t provide any kind of user interface.

For example, consider the processes shown in Figure 13-2.

> **NOTE**  Some system processes (but not all of them) are noted with a d at the end of the name, which stands for **daemon**.

![](bbox=[0.035, 0.825, 0.831, 0.968])