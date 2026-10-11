
## KEY TERMS

**GNOME Display Manager (gdm)** — A graphical login program that provides a graphical login screen.

**GNU Image Manipulation Program (GIMP)** — An open source graphics manipulation program that uses the GTK+ toolkit.

**GNU Object Model Environment (GNOME)** — The default desktop environment in Red Hat Fedora Linux; it was created in 1997.

**Grand Unified Bootloader (GRUB)** — A common boot loader used on Linux systems.

**grub-install command** — The command used to install the GRUB boot loader.

**grub-md5-crypt command** — The command used to generate an encrypted password for use in the /etc/grub/grub.conf file.

**GRUB root partition** — The partition containing the second stage of the GRUB boot loader and the /boot/grub/grub.conf file.

**GTK+ toolkit** — A development toolkit for C programming; it is used in the GNOME desktop and the GNU Image Manipulation Program (GIMP).

**init command** — The command used to change the operating system from one runlevel to another.

**initialize (init) daemon** — The first process started by the Linux kernel; it is responsible for starting and stopping other daemons.

**initstate** — *See also Runlevel.*

**K Desktop Environment (KDE)** — A desktop environment created by Matthias Ettrich in 1996.

**KDE Display Manager (kdm)** — A graphical login screen for users that resembles the KDE desktop.

**K Window Manager (kwin)** — The Window Manager that works under the KDE Desktop Environment.

**lilo command** — The command used to reinstall the LILO boot loader based on the configuration information in /etc/lilo.conf.

**Linux Loader (LILO)** — A common boot loader used on Linux systems.

**Master Boot Record (MBR)** — A small area normally located on the first sector of the first hard disk drive used to define partitions and a boot loader.

**maximum resolution** — The best clarity of an image displayed to the screen; it is determined by the number of pixels making up the image (for example, 640 × 480 pixels).

**Metacity Window Manager** — The default Window Manager for the GNOME Desktop Environment in Red Hat Fedora Core 2.

**mingetty** — A program used to display a login prompt on a character-based terminal.

**mouseconfig** — A command used to configure a mouse for use by X Windows.

**Multiuser Mode** — Also called runlevel 2; the mode that provides most daemons and a partial set of networking daemons.

**NTLOADER** — The boot loader used to boot Windows NT, Windows 2000, and Windows XP operating system kernels.

**ntsysv** — A utility that can be used to alter the daemons that are started in each runlevel.

**Power On Self Test (POST)** — An initial series of tests run when a computer is powered on to ensure that hardware components are functional.

**Qt toolkit** — The software toolkit used with the K Desktop Environment.

**runlevel** — A term that defines a certain type and number of daemons on a Linux system.

**runlevel command** — The command used to display the current and most recent (previous) runlevel.

**Single User Mode** — Also called runlevel 1; the mode that provides a single terminal and a limited set of services.

**system-config-display** — A command used to configure a video adapter card and monitor for use by X Windows.

**system-config-keyboard** — A command used to configure a keyboard for use by X Windows.

**system-config-mouse** — *See also Mouseconfig.*

**Tab Window Manager (twm)** — One of the oldest Window Managers used on Linux systems.

**telinit command** — An alias to the init command.

**vmlinuz-<kernel version>** — The Linux kernel file.

**Window Manager** — The GUI component that is responsible for determining the appearance of the windows drawn on the screen by X Windows.

**X client** — The component of X Windows that requests graphics to be drawn from the X server and displays them on the terminal screen.

**X Display Manager (xdm)** — A graphical login screen.

**Xfce desktop environment** — A desktop environment that is commonly used by Linux systems.

**XFree86** — A common implementation of X Windows used in Linux distributions.

**X.org** — A common implementation of X Windows used in Linux distributions.

**X server** — The component of X Windows that draws graphics to windows on the terminal screen.

**xvidtune** — A program used to fine-tune the vsync and hsync video card settings for use in X Windows.

**X Windows** — The component of the Linux GUI that displays graphics to windows on the terminal screen.

## Review Questions

1. Which of the following happens first during computer bootup?
   - a. The Linux kernel is loaded
   - b. BIOS performs the POST
   - c. BIOS checks its configuration in the CMOS chip on the mainboard for boot devices
   - d. Computer checks the master boot record

2. What is the last stage in the boot process when using the Grand Unified Boot loader (GRUB)?
   - a. 1
   - b. 1.5
   - c. 2
   - d. 2.5

3. What is the name of the first daemon process executed on the system after a boot loader loads the Linux operating system kernel into memory?
   - a. shell
   - b. proc
   - c. main
   - d. init

4. You can use X Windows on one computer to send graphical images to an X-client on an entirely different computer by changing the ________________ environment variable.
   - a. DISPLAY
   - b. HOST
   - c. WINDOW
   - d. XWINDOW

5. What is the Window Manager used for the GNOME desktop in Red Hat Fedora Core 2?
   - a. sawfish
   - b. kwin
   - c. metacity
   - d. mwm

6. True or false? The Linux boot loader is typically located on the first sector of an active Linux partition.

7. True or false? If you are using a Linux boot loader to dual boot another operating system in addition to Linux, it is easiest if Linux is installed after the other operating system has been installed.

8. True or false? Most daemons that are loaded upon system startup are executed from entries in /etc/inittab.

9. True or false? A typical installation of Red Hat Fedora Linux usually uses 1–2GB of data on the hard disk for the GUI and related programs.

10. True or false? When configuring monitor refresh rates, choosing an hsync or vsync value that is too high might result in headaches over time.

11. To uninstall LILO from an active partition or the MBR, you can use the `lilo - ____` command.

12. The ________ boot loader that is available with Windows NT, Windows 2000, Windows XP, and Windows Server 2003 can be used to display a screen at boot time that prompts the user to choose an operating system to boot.

13. A(n) ________ defines the number and type of daemons that are loaded into memory and executed by the kernel on a particular system.

14. The ________ Manager modifies the look and feel of X Windows.

15. To configure the mouse in Red Hat Fedora Linux, you can use either the GUI or system-config-mouse commands in either a GUI or terminal environment.

## Chapter 10

### Managing Linux Processes

After completing this chapter, you will be able to:

- Categorize the different types of processes on a Linux system
- View processes using standard Linux utilities
- Illustrate the difference between common kill signals
- Describe how binary programs and shell scripts are executed
- Create and manipulate background processes
- Use standard Linux utilities to modify the priority of a process
- Schedule commands to execute in the future using the at daemon
- Schedule commands to execute repetitively using the cron daemon

A typical Linux system can run thousands of processes simultaneously, including those that you have explored in previous chapters. In this chapter, you focus on viewing and managing processes. In the first part of the chapter, you examine the different types of processes on a Linux system and how to view them and terminate them. You then discover how processes are executed on a system, run in the background, and prioritized. Finally, you are introduced to the various methods used to schedule commands to execute in the future.

### Linux Processes

Throughout previous chapters of this book as well as in the workplace, the terms “program” and “process” have been and will be used interchangeably; however, there is a definite, yet fine, difference between these two terms. **A program** is an executable file on the hard disk that can be run when you execute it. **A process** refers to a program that is running in memory and on the CPU; in other words, a process is a program in action.

If you start a process while logged in to a terminal, that process runs in that terminal and is labeled a **user process**. Examples of user processes include `ls`, `grep`, `find`, and most other commands that you have executed throughout this book. Recall that a system process that is not associated with a terminal is called a **daemon process**; those processes are typically started on system startup, but you can also start them manually. Most daemon processes provide system services, such as printing, scheduling, and system maintenance, as well as network server services, such as Web servers, database servers, file servers, and print servers.

Every process has a unique **process ID (PID)** that allows the kernel to identify it uniquely. In addition, each process can start an unlimited number of other processes called **child processes**. Conversely, each process must have been started by an existing process called a **parent process**. As a result, each process has a **parent process ID (PPID)**, which identifies the process that started it. An example of the relationship between parent and child processes is depicted in Figure 10-1.

![](img/09bf13b782f71165e17bb3839040c96a_393_0.png)

> PIDs are not necessarily given to new processes in sequential order; each PID is generated from free entries in a process table used by the Linux kernel.
> 
> Remember that although each process can have an unlimited number of child processes, it can only have one parent process.
