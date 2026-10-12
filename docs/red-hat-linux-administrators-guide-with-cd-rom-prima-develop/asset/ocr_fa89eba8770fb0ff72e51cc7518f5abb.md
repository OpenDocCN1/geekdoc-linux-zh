# STARTING UP AND SHUTTING DOWN



A command such as this verbosely checks the root file system as defined by your system setup (hence the -v) or / and corrects the errors. This command uses the default file system type of ext2 (the -t flag sets the file system type).

By the same token, the command fsck by itself and the file system name will accomplish the same purpose without the flags or options.

```
```bash
fsck /dev/hda1
```
```

The fsck command exists on other systems as well and can be used for a variety of other file system types. Consulting the man pages before executing any command involving fsck is always a good idea.

# ## Understanding Kernel Panics

In the case of a kernel panic, or when the boot sequence fails to load the kernel correctly and the machine cannot start correctly, you cannot do much to get the computer operative without making changes to the kernel. Upon bootup, an error message saying “Kernel Panic” will usually be followed by additional information stating what might have caused the system to halt. An error such as this indicates a bad kernel or one that cannot read the available options on the system or cannot read them as they are set up in the kernel.

Several things can cause a kernel panic. Often such a panic results from a customized kernel that was built without some necessary content. When building any sort of custom kernel, it is best to have a backup kernel in case things go wrong. A reboot to the previous kernel will usually solve the problem until a properly configured kernel can be compiled.

Improperly loaded kernel modules can also cause a kernel panic, whether they are for a SCSI device, an improper file system type, or loss of disk partitions. It is always wise to keep some sort of backup handy for cases when the system goes down or when the system does not reboot normally. The best thing to do in these instances is to attempt to reboot the machine with another kernel, whether it be the default or a backup. You can also use the Red Hat boot disk to gain a root prompt or create a Linux rescue disk during the installation routine. If you can get to a root prompt in any manner, then you should be able to correct the problem. I suggest taking enough precautions by adding *golden kernels*, or kernels that have proven trustworthy, and by editing the /etc/lilo.conf file to allow for backup options. If none of these alternatives are available, a most unlikely scenario, a reinstall may be your only choice. I have found it easier in the long run to