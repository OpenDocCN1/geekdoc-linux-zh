
VMware is an interesting and potentially useful scenario where you need to have access to Linux applications from Windows, or if you require access to Windows applications while working within Linux. VMware uses terminology such as *host operating system*, which is the term meaning the operating system that’s running the VMware product, and *guest operating system*, which is the term that refers to the operating system that’s being run under VMware itself. VMware even allows you to run the guest operating system in full screen mode, as well as the ability to switch back to a windowed mode by pressing Ctrl+Alt+Esc.

## Chapter 4
### Booting and Shutting Down
### IN THIS CHAPTER
- Understanding how the boot process works
- Understanding run levels and their role in the boot process
- Booting up your system
- Shutting down your system
- Rebooting your system
- Configuring the init process
- Managing init scripts

Red Hat Linux uses a highly configurable boot and shutdown process that needs to be understood by every Linux system administrator. There are many configuration options and files involved in the boot process that enable you to fine-tune which run level (single user, multiuser, graphical) the system boots to, what programs get started, how the network is configured, and so on. In this chapter you will get up to speed on the boot and shutdown processes.

### Understanding the Boot Process
When you turn on your Linux system (or *boot* it) Linux looks to various files and programs — notably the `init` program and `/etc/inittab` file — for instructions on how to load your system, which services to start (and which not to), whether or not to start the X Window System, and so on. The init command is highly customizable; with init you can choose which programs and services run as part of the boot process. init is covered in detail in later sections of this chapter, but before you start looking hard at init you should have a basic understanding of how LILO and init work together to start your computer. The following list discusses the basic process that occurs whenever you boot up your Linux system.

- 1. The Red Hat Linux kernel (the kernel is the core operating system) is typically stored in a compressed file on your hard drive. When you first turn on your computer, the kernel is started by a boot loader program like LILO or GRUB.
- 2. After being started by LILO, the kernel uncompresses itself, initializes the display device, and starts checking other hardware attached to your computer.
- 3. As Linux finds your hard drives, floppy drives, network cards, and so forth, it loads the appropriate device driver modules. During this process it prints out text messages on your console screen.

![](img/9eb7e89292d2f85707b4d49102c865b7_93_0.png)

If you are at the console when booting your system, you can press Shift+PageUp to scroll back the display to view boot messages. You can also view the boot messages at any time after system startup by running the dmesg program. The /var/log/messages files will also have many of the boot messages.

- 4. The kernel mounts the root file system (/) as read only and performs checks on the file system.
- 5. If everything checks out okay, the root file system is then typically mounted as read/write. If a problem arises and the kernel fails to mount the root partition or finds a severe problem with it, the kernel panics and halts the system. If the disk has become corrupt for some reason, the kernel might provide you an option to run a file system checker program such as fsck.ext2 from a restricted shell.
- 6. After the root file system is mounted, the kernel starts a program called init. init in turn starts all other programs required for the user to log in to the system, including the login programs. After init has started all the necessary programs, the system is up and running and the boot process is complete.

### Understanding Run Levels
At any given time a Linux system is running in a known state or level, which is called a run level. Table 4-1 shows the list of possible run levels. For example run level 0 refers to the state when the system is halted, run level 1 is the single-user state where none of the networking or multiuser capabilities of Linux are available.

Table 4-1 Possible Run Levels in a Linux System

| Run Level | Description |
|---|---|
| 0 | Halt – used to halt the system. Never set the system default run level to this or else you won't be able to boot your system. |
| 1 | Single-user – used to set the system in a minimal configuration suitable for a single user. |
| 2 | Not used. |
| 3 | Multiuser – used to set the system in a configuration that supports multiple users. |
| 4 | Not used. |
| 5 | Used to start the X Window System and the xdm, kdm, or gdm programs via /etc/X11/prefdm script. |
| 6 | Reboot – used to reboot the system. |
| S or s | Used internally by scripts that run in run level 1. |
| a, b, c | On-demand run levels – typically not used. |

The init program allows you to switch from one run level to another. It is discussed in the "Configuring init" section later in this chapter.

### Booting Up Your System
During the boot process, init first runs the rc.sysinit script and then runs the script for the default run level. You can set the default run level in /etc/inittab by changing the line in /etc/inittab file:

```
id:3:initdefault:
```

Here the default run level is set to 3, meaning that init runs the scripts needed to put the system in multiuser mode.

If you take a second look at /etc/inittab, you will notice that the following line specifies which rc script needs to be run for run level 3.

```
13:3:wait:/etc/rc.d/rc 3
```

The rc script is run with an argument of 3. As mentioned before, this script runs all the scripts whose names start with “S” in the /etc/rc.d/rc3.d directory. It also supplies “start” as an argument to each of the “S”-prefixed scripts. When all the “S” scripts are run, the rc script finishes and the system becomes available in the default run level.

### Booting to single-user mode
Booting to single-user mode is usually necessary in case of emergencies, such as when you need to fix a corrupt disk or reset a forgotten root password. Whatever the reason, you have two ways to boot in single-user mode.

If you're already logged into the system and want to switch to single-user mode, you can run the following command:

```
init 1
```

This tells init to switch run level to 1, which is the single-user mode. However, if you plan on getting access to the system in single-user mode when it is actually booting up, then at the LILO prompt enter:

```
linux single
```

This boots Linux to single-user mode.

![](img/9eb7e89292d2f85707b4d49102c865b7_95_0.png)

> If you are using graphical LILO prompt, you can press Ctrl+X to summon the text LILO prompt from which you can enter the above command.

### Booting in rescue mode
If your Linux system does not boot for some reason and you wish to try and rescue the system, you can boot the system in rescue mode if you have the official Red Hat CD-ROM.

Follow these steps to do so:

- 1. Insert the Red Hat CD-ROM that you bought into the CD-ROM drive and make sure that your computer’s BIOS has been set up to boot from CD-ROM first. If it hasn’t been set up for this, simply reboot your system and go inside your BIOS utility and set the boot device option to boot from the CD-ROM first. Then reboot the machine with the official Red Hat CD-ROM inside the CD-ROM drive.
- 2. After the system displays the initial Linux installation screen in multicolored text, choose rescue mode by entering `linux rescue` at the LILO prompt.
- 3. You’re then asked to select a language. Select English or whatever language you use and then press Enter to continue. The system will be mounted under `/mnt/sysimage`, and you can then press Enter to summon a shell prompt.
- 4. At the shell prompt you can use tools that are available in `/sbin` or `/usr/bin` directories to perform any necessary rescue operations. For example, if your password file (`/mnt/sysimage/etc/passwd`) was deleted by accident you can potentially rescue it from an older version by copying `/mnt/sysimage/etc/passwd` to `/mnt/sysimage/etc/passwd` or any other backup you have. If a disk problem caused your system to fail and you want to know how to access your disk partitions, first run `cat /etc/mtab` or `cat /proc/mounts` to see which partition of your disk is mounted at what directory under `/mnt/sysimage`. Then you can perform disk commands such as `fsck` on the appropriate partition. For example, if the `/usr` partition on your regular system caused the system to become unbootable, you can run `fsck /mnt/sysimage/usr` in rescue mode to isolate the problem with the disk and attempt to fix it.
- 5. After you exit the shell prompt by entering `exit` at the prompt, the system reboots automatically.
