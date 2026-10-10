![](bbox=[0.14, 0.1, 0.35, 0.27])

So far, this book has dealt largely with a running Linux system, but from time to time, you’ll need to boot Linux. Ordinarily this process is a painless one: You press the power button, wait a couple of minutes, and see a Linux login prompt. Sometimes, though, you’ll have to intervene in this process in one way or another.

Linux boot loaders can be configured to boot Linux with particular options and even to boot other operating systems, so knowing how to configure them and use them can help you to accomplish your boot-related goals. Once the system is booted, you should know how to study log files related to the boot process. This can help you to diagnose problems or verify that the system is operating the way it should be.

Finally, this chapter looks at editing files with Vi. Vi isn’t particularly boot-related, knowing how to edit files is vital to many administrative tasks, including editing the boot loader configuration files.

# ## Installing Boot Loaders

Hard disks contain more than partitions and their contents. One very small part of the disk is unusually important: The *master boot record* (MBR) contains the MBR partition table and a *boot loader* (also sometimes called a *boot manager*). The boot loader is the software that the BIOS reads and executes when the system begins to boot. The boot loader, in turn, is responsible for loading the Linux kernel into memory and starting it running. Thus, configuring a hard disk (or at least your boot hard disk) isn’t complete until the boot loader is configured. Although Linux distributions provide semi-automated methods of configuring a boot loader during system installation, you may need to know more, particularly if you recompile your kernel or need to set up an advanced configuration—say, one to select between several OSs.

In practice, two boot loaders are important in Linux: the *Linux Loader* (LILO) and the *Grand Unified Boot Loader* (GRUB). LILO is older, and it’s slowly being replaced by GRUB as the most common Linux boot loader, but LILO is still common.

![](bbox=[0.14, 0.82, 0.22, 0.87])

> **NOTE** LILO and GRUB are both x86 and x86-64 boot loaders. Other platforms have their own boot loaders. Some of these are similar to LILO in operation (and may even be called LILO), but they aren’t quite identical. You should consult platform-specific documentation if you need to reconfigure a non-x86 boot loader.