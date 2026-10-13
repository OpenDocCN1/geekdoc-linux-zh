![](bbox=[0.153, 0.098, 0.243, 0.161])

In some Solaris documentation, pseudo or memory-based file systems are referred to as “virtual file systems.” However, this term is also used for file systems created and managed by virtual disk management systems (covered in Chapter 15, “Advanced Disk Management”). To avoid confusion, I refer to memory-based file systems only as “pseudo file systems.”

# Process File System (PROCES)

The Process File System is a memory-based file system used to provide process status and information. One instance of PROCFS exists on a system by default; it is accessible as the /proc directory. This directory contains one directory for each active process on the system. The directory name is the process ID (PID) of the process. Files under each PID directory provide various status and other information about the process. The /proc directory is owned by the root account and has an access mode of 555 (read/execute for owner/group/other) because no user account (not even root) should attempt to modify the files. These files are managed directly by the kernel.

# The Proc Tools

You extract process status and other information from the /proc PROCFS instance by using the proc tools, which are a collection of command-line utilities. These tools also provide stop/start capability.

The PID of the process to be examined is specified as a command-line argument. If more than one process is to be examined, the PIDs should be separated by spaces. Table 16.2 provides a list of the proc tools.

![](bbox=[0.153, 0.605, 0.243, 0.67])

Be familiar with the names and purposes of the proc tools. Memorizing Table 16.2 should be sufficient.

| Command | Purpose |
|---|---|
| `pcred` | Lists process credentials (effective and real UID and GID) |
| `pflags` | Displays tracing flags and pending and held signals, along with other information |
| `pfiles` | Lists information on all open files |
| `pldd` | Lists dynamic link libraries used |
| `pmap` | Displays the memory address space map |
| `prun` | Restarts the process |