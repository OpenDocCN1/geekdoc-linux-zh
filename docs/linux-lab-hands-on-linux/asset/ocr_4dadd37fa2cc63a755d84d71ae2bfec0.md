# **05** LAB: Linux Process Management

**OBJECTIVES**

+   1.  Understaing various type of Processes in Linux.
+   2.  Understanding different commands in Linux processes

**REQUIREMENTS**

A standard PC with installed Linux operating system (such as Fedora, RHEL).

**CONCEPT**

The Linux process management always starts with the init command. You can start any process with this command. You can use ps command to display currently process on Unix/Linux operating system. If you want to stop any running process you can execute the kill command. If you want to killall process simutaneously use the killall command.

# Type Processes in Linux

Various type of processes in Linux are as follows:

+   ## init
+   init command is the initiates all processes. Its primary role is to create processes from a script stored in the file /etc/inittab. This /etc/inittab file usually has entries that enable the users log in. It also controls autonomous processes required by any particular system.
+   
+   When a Linux system is booted, GRUB.conf loads the kernel. The kernel in turn runs the init program, which is the first process to run on the system. The init program can start other processes depending on the system's run level. Every process on the Linux system gets a process identification (PID) number. Since init is always the first process loaded into memory, it has a PID of 1.

+   ## Daemon Process
+   A daemon process is a process that runs continually on your system or is loaded into memory only when asked to do so. You can load several daemon processes into memory during the Linux bootup. The examples of common daemon processes are dhcpd (Dynamic Host Configuration Protocol Daemon), crond (Cron Daemon), and lpd (Line Printer Daemon). A daemon process is usually identified by the letter d at the end of the process name.