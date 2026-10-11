# LILO

LILO (LI**n**ux LOader) is a boot loader that can reside on your hard disk or your boot floppy. It is executed when the system boots. Features of **LILO** include the following:

+   - Will work with DOS, UNIX, OS/2, Windows 95/98, and Windows NT
+   - Replaces the master boot record on your hard drive
+   - Can use up to 16 different boot images on different partitions, each of which can be password protected
+   - Allows the boot sector file, map file, and boot images to reside on different partitions

LILO has the capability to act as a boot loader for other operating systems. It will allow you to select the operating system you wish to boot.

> **Key Concept**
> LILO provides an efficient method for booting Linux as well as other operating systems. LILO can handle up to 16 different boot images on a single hard disk.
> When you install LILO, you can select to overwrite the Master Boot Record or not.

If no selection is made, the default operating system is usually booted. You can bypass this action by either pressing a key (the Alt, Shift, or Ctrl key) or requesting a prompt in the /etc/lilo.conf file. Either of these actions will cause LILO to show a boot prompt:

BOOT:

At this point, you can type the name of the operating system to boot. If you press Tab or type ? at the LILO boot prompt, a list of configured operating systems will be displayed. If you do not make a selection, LILO will boot the first operating system it finds.

When typing a selection at the boot prompt, you can pass options to the kernel. This is often used to start your system in single-user mode by typing

```
kernelName single
```

at the boot prompt. Other options that can be passed include root=device, ro for read-only, and rw for read-write.

How LILO behaves is controlled by its default configuration file, /etc/lilo.conf. The LILO command has several different uses; its syntax is

```
lilo [options]
```