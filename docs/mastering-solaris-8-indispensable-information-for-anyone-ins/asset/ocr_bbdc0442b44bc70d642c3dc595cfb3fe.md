The Solaris operating system installs in five different forms, with five different base sizes:

+   - The core Solaris system is 205MB.
+   - The end user system (64 bit) is 562MB.
+   - The developer system (64 bit) is 922MB.
+   - The entire system (64 bit) is 980MB.
+   - The entire system with additional original equipment manufacturer (OEM) support is 988MB.

Most systems these days have disks greater than 2GB, and so you are encouraged to install the complete Solaris distribution on your system whenever possible. If you plan on using additional hardware such as add-in cards, you may need to also install OEM support.

In deciding to partition your system, you need to consider how many users are going to be working on it. For a single-user system, you may want to create a large partition on your disk for the root partition; for a multiser system, you may want to create additional partitions to protect the system from problems that might arise. One of the two most troublesome problems you'll encounter is that a user can fill up a partition and, if it is a single partition, the system will slow down considerably. Unlike other operating systems, Solaris will not crash when the disk is full. Solaris reserves about 5 percent of the space on the root partition for the system administrators' use, which allows system maintenance to restore the system to good working order. In a multiserver situation, you can set on users' disk quotas that allow you to control how much disk space any user can consume.

The second problem you'll encounter related to Solaris, one that is generally true of all Unix systems, is that you may over time have a rogue daemon fill up a partition by creating a large log file. A rogue daemon is not necessarily a virus, although it is entirely possible that it could be. In the Unix world, due to strict system security, it is hard for a process to obtain root privileges from the outside and make a system unusable. Much more common is the process by which a system utility is given root privileges by an administrator to track events or processes and then writes to a log file. When that rogue daemon runs as root and consumes all available disk space, the system can either become inaccessible or perform too slowly to be useful. In some instances, you may find that you will need to use the Solaris installation CD-ROM to restore the system to use.

To some extent, you can use partitioning to help you with these two problems. Partitioning segments your hard drive into different areas that are used by different directories. You can use the Solaris security scheme to restrict users and processes like