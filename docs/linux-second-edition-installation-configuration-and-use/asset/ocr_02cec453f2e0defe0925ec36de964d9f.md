In order to prevent problems with access and ownership rights, you must ensure that /etc/passwd and /etc/group are synchronized on all computers. For all computers, the same UID and GID numbers must apply. (In large networks, this can be achieved through NIS or rpc.bindd.)

In kernel 2, the locking behavior of NFS has changed. If you encounter locking problems, you can remedy them by means of the nolock option in mount or fstab.

# # 6.10 Boot diskettes/LILO

To be precise, in this section, 'boot process' only means the start of the kernel and access to the root partition. Once this has succeeded, the system is initialized. This is the responsibility of the /sbin/init program, which is started by the kernel as the very first process to run. (The Init V process is too often considered as part of the boot process. More information on the Init process can be found on page 124 onward.

For booting, the Linux kernel must be able to be loaded from a diskette or a hard disk. If the root partition is located on a SCSI disk, the kernel must include the appropriate SCSI driver. Other drivers may be loaded as modules at a later stage - but only after access to the root partition is working. The only exception to this rule is to load the SCSI driver into a RAM disk during booting and activate it from there as a module. RedHat has this booting concept in its default configuration. The advantage of this process is that it can be configured without recompiling the kernel.

There are many ways to boot Linux:

+   - The easiest but slowest variation is loading the kernel from a boot diskette. (see page 181).

+   - Using a boot diskette with LILO is already somewhat elegant. Only the tiny LILO program (that is, the Linux Loader) boots from the diskette. It accesses the hard disk and loads the kernel from there. LILO fundamentals are discussed from page 183 onward; LILO installation on a diskette is described on page 189.

+   - An more elegant solution is to install LILO itself on the hard disk. This, however, is not entirely without problems, since conflicts with other operating systems may occur. Page 191 describes not how to install LILO into the MBR (Master Boot Record), but also how to create a backup copy of this sector beforehand.

+   - Usually, the kernel file loaded by LILO is located in a Linux partition. If this partition starts in a sector that can no longer be reached by the BIOS (1024-cylinder limit), the kernel and the other boot files can also be installed in a DOS partition - see page 193.

![](bbox=[0.215, 0.063, 0.335, 0.223])