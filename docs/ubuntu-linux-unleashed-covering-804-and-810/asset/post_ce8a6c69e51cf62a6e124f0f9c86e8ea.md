
This next step of the boot process begins with a message that the Linux kernel is loading, and a series of messages will be printed to the screen, giving you the status of each command. A failure should display an error message. The -quiet option may be passed to the kernel at boot time to suppress many of these messages.

If the boot process were halted at this point, the system would just sit idle and the screen would be blank. In order to make the system useful for users, we need to start the system services. Those services are some of the applications that allow us to interact with the system.

## System Services and Runlevels

The init command boots Ubuntu to a specific system state, commonly referred to as its runlevel.

Runlevels determine which of the many available system services are started, as well as in which order they start. A special runlevel is used to stop the system, and a special runlevel is used for system maintenance. As you will see, there are other runlevels for special purposes.

You will use runlevels to manage the system services running on your computer. All these special files and scripts are set up during your installation of Ubuntu Linux, and they receive their initial values based on your choices during the installation—as described in Chapter 3, “Installing Ubuntu,” and Chapter 4, “Post-Installation Configuration.” You can change and control them manually, as you learn later in this chapter using tools of varying sophistication.

## Runlevel Definitions

The Ubuntu runlevels are defined for the Ubuntu system in /etc/init.d.

Each runlevel tells the init command what services to start or stop. Although runlevels might all have custom definitions, Ubuntu has adopted some standards for runlevels:

- Runlevel 0—Known as “halt,” this runlevel is used to shut down the system.
- Runlevel 1—This is a special runlevel, defined as “single,” which boots Ubuntu to a root access shell prompt where only the root user may log in. It has networking, X, and multi-user access turned off. This is the maintenance or rescue mode. It allows the system administrator to perform work on the system, make backups, or repair configuration or other files.
- Runlevel 2—This is the default runlevel for Ubuntu.
- Runlevels 3–5—These runlevels aren’t used in Ubuntu but are often used in other Linux distributions.
- Runlevel 6—This runlevel is used to reboot the system.

Runlevel 1 (also known as single-user mode or maintenance mode) is most commonly used to repair file systems and change the root password on a system when the password has been forgotten. Trespassers with physical access to the machine can also use runlevel 1 to access your system.

**CAUTION**
Never forget that uncontrolled physical access is virtually a guarantee of access to your data by an intruder.

## Booting into the Default Runlevel

Ubuntu boots into runlevel 2 by default, which means it starts the system as normal and leaves you inside the X Window System looking at the Gnome login prompt. It knows what runlevel 2 needs to load by looking in the rc*.d directories in /etc. Ubuntu contains directories for rc0.d through to rc5.d and rc6.d.

Assuming that the value is 1, the rc script then executes all the scripts under the /etc/rc.1 directory and then launches the graphical login.

If Ubuntu is booted to runlevel 1, for example, scripts beginning with the letter K followed by scripts beginning with the letter S under the /etc/rc1.d directory are then executed:

```
# ls /etc/rc1.d/
K01gdm        K19hplip      K20laptop-mode   K20vsftpd     K80slapd
K01usplash    K20acpi-support K20makedev      k21acpid      K86ppp
...etc...
K19cupsys     K20inetutils-inetd K20ssh        K74-bluez-utils S20single
```

These scripts, as with all scripts in the rc*.d directories, are actually symbolic links to system service scripts under the /etc/init.d directory.

The rc1.d links are prefixed with a letter and number, such as K15 or S10. The (K) or (S) in these prefixes indicate whether or not a particular service should be killed (K) or started (S) and pass a value of stop or start to the appropriate /etc/init.d script. The number in the prefix executes the specific /etc/init.d script in a particular order. The symlinks have numbers to delineate the order in which they are started. Nothing is sacred about a specific number, but some services need to be running before others are started. You would not want your Ubuntu system to attempt, for example, to mount a remote Network File System (NFS) volume without first starting networking and NFS services.

## Booting to a Non-Default Runlevel with GRUB

There might come a time when you do not want to boot into the default runlevel, such as when you want to repair the X server or install a new graphics driver. You'll need to follow several specific steps to boot to a non-default runlevel if you use the default boot loader for Ubuntu, GRUB.
