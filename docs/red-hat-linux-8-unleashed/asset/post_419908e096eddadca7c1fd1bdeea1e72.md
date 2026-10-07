
# CHAPTER 7 Managing Services

Note that this chapter covers the basic operating system, not the details of the multitude of special services that can run on a system such as File Transfer Protocol (FTP), or the Apache Web server. Those administration details are contained in separate chapters.

# Understanding the Red Hat Linux Boot Process

Although the actual boot loading mechanism for Linux varies on different hardware platforms (such as the SPARC, Alpha, or PowerPC systems), Intel-based PCs running Red Hat Linux most often use the same mechanism throughout product lines. This process is accomplished through a Basic Input Output System, or BIOS. The BIOS is an application stored in a chip on the motherboard that will initialize the hardware on the motherboard (and often the hardware that's attached to the motherboard). The BIOS also gets the system ready to run and load the software that we recognize as the operating system.

Finally, the BIOS code looks for a special program known as a bootloader or boot code. The instructions in this little bit of code tell the BIOS where the Linux kernel is located, how it should be loaded into memory, and how it should be started.

# Beginning the Boot Loading Process

If it goes well, the BIOS looks for a bootable volume (or disk), which is containing one special hexadecimal value written to the volume by the boot loader application when the boot loader code was first installed in the system's drives, in the order established by the BIOS settings (for example: the floppy first, followed by a CD-ROM, and then a hard drive, booting from the first bootable volume it finds).

> If the BIOS detects a hardware problem, the process will fail and the BIOS will generate a few beeps from the speaker. These "beep codes" can indicate the nature of the problem the BIOS has encountered. The codes vary among manufacturers, and the diagnosis of problems occurring during this phase of the process is beyond the scope of this book. If you encounter a problem, you should consult the motherboard manual or contact the manufacturer of the motherboard.

Next, the BIOS looks on that for boot code in the partition boot sector, also known as the Master Boot Record (MBR) of the first hard disk. The MBR contains the boot loader code and the partition table—think of it as an index for boot, plus a few comments. (We cover the MBR in more detail in Chapter 10, "Managing the Filesystem.") If the BIOS finds a boot loader, it loads the code into memory. At that point, the BIOS's job is completed, and it passes control of the system to the boot loader.

The boot loader locates the Linux kernel on the disk and loads it into memory. After that task is completed, the boot loader passes control of the system to the Linux kernel. You can see how one process builds upon another in an approach that allows many different operating systems to work with the same hardware.

# Understanding the Red Linux Boot Process

Red Hat Linux can use a variety of boot loaders, including GRUB (the default for Red Hat), LILO (a long-time standard and available for use in Red Hat), BootMagic (a commercial program), and others.

> NOTE
Linux is very flexible and can be booted from multiple images on a CD-ROM, over a network using PXE or NetBoot, on a headless server with the console display sent over a serial or network connection. There is even work underway to create a special Linux BIOS at http://www.acl.linux.org/linuxbios/.

This kind of flexibility allows Linux to be used in a wide variety of ways, such as remote servers or workstations, that are not generally seen in personal home use.

# Loading the Linux Kernel

In general, the kernel manages the system resources. UNIX refers to each application as a process and the kernel assigns each process number called a PID, or process ID. First, the Linux kernel loads and runs a process name init—also known as the “father of all processes” because it starts for every subsequent process. The init process looks for a list of instructions in a file named /etc/rc.d/rc.sysinit. That script issues a number of commands that are only run once—each time the system is turned on.

> NOTE
Details about the sequence of events that occur when the Linux kernel is loaded can be found in the file /usr/src/linux-2.4/init/main.c if you have installed the Linux kernel documentation.

This step of boot process begins with a message that the Linux Kernel is loading, and a series of messages should be printed to the screen, giving you the status of each command in the rc.sysinit script. A failure should display an error message.

Although it's not intended to modify the rc.sysinit script, knowledge of the contents of the file might aid you in diagnosing a problem if the boot process fails during this step. Have a look at rc.sysinit, and you'll discover it's a text file filled with shell scripts. (You can learn about scripting in Chapter 22, “Shell Scripting”)

After the rc.sysinit script has been run, the basic system is configured and the kernel is in control of the system. If the boot process were halted at this point, the system would just sit idle and the screen would be blank. In order to make the system useful for us, we need to start the system services. Those services are some of the applications that allow us to interact with the system.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Red Hat Linux Runlevels

After finishing with rc.sysinit during the booting process, the init command uses the Linux system initialization table found in /etc/inittab to boot Red Hat Linux to a specific state. The state of the system is referred to as its runlevel.

Several different ways of starting and stopping system services exists, and Red Hat uses a method derived from System V UNIX. The System V method uses runlevels and different combinations of services to define different states.

# Booting into the Default Runlevel

Entries in /etc/initab use a field-based notation that determines the runlevel—when to execute the process, whether or not the process is executed when booting, whether or not
