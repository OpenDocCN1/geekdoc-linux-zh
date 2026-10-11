
## Review Questions

- 1. What symbol is used to redirect to standard output in the BASH shell?
  - a. #
  - b. ?
  - c. >
  - d. ~
- 2. What is the pipe shell metacharacter?
  - a. |
  - b. >
  - c. &
  - d. @
- 3. Most variables in the shell are referred to as **environment** variables because they are typically set by the system and contain information that the system and programs access regularly.
  - a. shell
  - b. environment
  - c. system
  - d. user-defined
- 4. The **PATH** variable is one of the most important variables in the BASH shell, as it allows users to execute commands by typing the command name alone.
  - a. BIN
  - b. HOME
  - c. PWD
  - d. PATH
- 5. The **case** statement compares the value of a variable with several different patterns of text or numbers.
  - a. &&
  - b. case
  - c. ||
  - d. if
- 6. True or false? Input redirection must occur at the beginning of the pipe and output redirection must occur at the end of the pipe.
- 7. True or false? The `sed` command can only be used to perform a global search and replace.
- 8. True or false? The `awk` command treats each line of text as a record in a database, and each word in a line as a database field.
- 9. True or false? To change the value of a variable, you specify the variable name followed immediately by the new value.
- 10. True or false? You cannot create aliases to multiple commands.
- 11. Command input and output are represented by labels known as file ___________________.
- 12. The ___________________________ filter command numbers lines in a file.
- 13. To display a user's working directory the command `echo` _______________________________ would be used.
- 14. Most commands that are run by the shell are run in a separate ____________________________, which is created by the current shell.
- 15. To see a list of all exported environment and user-defined variables in the shell, you can use the ________________________ command.

# Chapter 9 System Initialization and X Windows

After completing this chapter, you will be able to:
- Summarize the major steps necessary to boot a Linux system
- Configure the LILO and GRUB boot loaders
- Dual boot Linux with the Windows operating system using LILO, GRUB, and NTLOADER
- Understand how the init daemon initializes the system at boot time into different runlevels
- Configure the system to start daemons upon system startup
- Explain the purpose of the major Linux GUI components: X Windows, Window Manager, and desktop environment
- List common Window Managers and desktop environments used in Linux
- Configure X Windows settings using various Linux utilities

Earlier in this book, you installed the GRUB boot loader for the Linux kernel during the Red Hat Fedora installation program. In this chapter, you investigate the boot process in greater detail. You explore the different types and configurations of boot loaders, as well as the process of dual booting the Linux operating system with the Windows operating system. Later in this chapter, you learn the procedure used to start daemons after the kernel has loaded and how to manipulate this procedure to start and stop new daemons. Finally, you examine the various components the Linux GUI comprises, and how to configure the Linux GUI using common Linux utilities.

## The Boot Process

When a computer first initializes, the BIOS on the mainboard performs a **Power On Self Test (POST)**. Following the POST, the BIOS checks its configuration in the CMOS chip on the mainboard for boot devices to search for and operating systems to execute. Typically, computers first check for an operating system on floppy disk and on CD-ROM devices present in the computer and contain a disk. This ensures that installation of an operating system from CD-ROM or floppy disk can occur at boot time. After these two devices are checked for an operating system, the computer usually checks the **Master Boot Record (MBR)** on the first hard disk inside the computer.

![](img/09bf13b782f71165e17bb3839040c96a_344_0.png)

**NOTE**
Recall that you can alter the order in which boot devices are checked in the computer BIOS.

The MBR might have a **boot loader** on it that can then locate and execute the kernel of the operating system. Alternatively, the Master Boot Record might contain a pointer to a partition on the system that contains a boot loader on the first sector; the partition to which the Master Boot Record points is referred to as the **active partition**. There can be only one active partition per hard disk.

Regardless of whether the boot loader is loaded from the Master Boot Record or the first sector of the active partition, the remainder of the boot process is the same. The boot loader then executes the Linux kernel from the partition that contains it.

**NOTE**
The Linux kernel is stored in the */boot* directory and is named *vmlinuz-<kernel version>*.

After the Linux kernel is loaded into memory, the boot loader is no longer active; instead, the Linux kernel continues to initialize the system by loading daemons into memory. A **daemon** is simply a system process that performs useful tasks, such as printing, scheduling, and operating system maintenance. The first daemon process on the system is called the **initialize (init) daemon**; it is responsible for loading all other daemons on the system required to bring the system to a usable state in which users can log in and interact with services. The whole process is depicted in Figure 9-1.

![](img/09bf13b782f71165e17bb3839040c96a_345_0.png)

## Boot Loaders

As discussed in the previous section, the primary function of boot loaders during the boot process is to load the Linux kernel into memory. However, boot loaders can perform other functions as well, including passing information to the kernel during system startup and booting other operating systems that are present on the hard disk. Using one boot loader to boot one of several operating systems is known as dual booting; the boot loader simply loads a different operating system kernel based on user input.

Although you can use many different boot loaders to boot Linux, the two most common boot loaders used on Linux systems today are LILO and GRUB.

**NOTE**
Only one operating system can be active at any one time.

### LILO

Linux Loader (LILO) is the traditional Linux boot loader. Although it can reside on the first sector of an active Linux partition, it is typically located on the Master Boot Record of the hard disk. When the computer completes the POST and locates the LILO boot loader, a LILO boot: prompt appears. You can then press the Tab key to see a list of operating systems that you can boot. Following this, you can enter the name of an operating system and press Enter, press Enter to boot the default operating system (usually Linux), or wait five seconds for the system to boot the default operating system automatically.

After the operating system is fully loaded, you can configure the LILO boot loader by editing the /etc/lilo.conf file; an example of this file is shown next:

```bash
[root@server1 root]# cat /etc/lilo.conf

prompt
timeout=50
default=linux
boot=/dev/hda
map=/boot/map
install=/boot/boot.b
lba32
image=/boot/vmlinuz-2.6.5-1.358
label=linux
initrd=/boot/initrd-2.6.5-1.358.img
read-only
append="rhgb quiet root=/dev/hda1"

[root@server1 root]# 
```

The preceding /etc/lilo.conf file indicates that LILO boots the linux kernel /boot/vmlinuz-2.6.5-1.358 provided the user chooses the operating system name linux (label=linux). Furthermore, the system continues to boot the default operating system (default=linux) if the user does not enter any input for five seconds (timeout=50). And furthermore, the LILO boot loader tells the Linux kernel to use a Red Hat Graphical Boot after it has loaded (rhgb), suppress detailed kernel messages (quiet), and mount the root filesystem on /dev/hda1 (root=/dev/hda1).

**NOTE**
You can also use root=LABEL=/ instead of root=/dev/hda1 in the preceding example to force LILO to read the appropriate entry from the /etc/fstab file for the root filesystem.
