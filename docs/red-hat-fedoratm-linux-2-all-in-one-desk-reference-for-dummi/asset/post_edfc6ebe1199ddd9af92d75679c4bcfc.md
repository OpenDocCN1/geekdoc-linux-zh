
# Resolving Other Installation Problems

![](img/9f89727199836b0f871f1745838aa8b2_87_0.png)

The `Xorg.conf` file created by using the `-configure` option of the X server does not display at the best resolution possible. To fine-tune the configuration file, run the Display Settings utility (choose Main Menu::System Settings:: Display) after you reboot the system. By using that utility, you can configure the video card, monitor, and display settings through a graphical user interface.

## Resolving Other Installation Problems

I'm sure I haven't exhausted all the installation problems that are lurking out there. Nobody can. There are so many different combinations of components in Intel x86 PCs that Murphy's Law practically requires some combination of hardware to exist that the installation program can't handle. This section lists a few known problems. For others, I advise you to go to Google Groups (`groups.google.com`) and type in some of the symptoms of the trouble. Assuming that others are running into similar problems, you can get some indication of how to troubleshoot your way out of your particular predicament.

## The fatal signal 11 error

Some people get a fatal `signal 11 error` message during installation — and it stops the process cold. This error usually happens past the initial boot screen as the `anaconda` installer is starting its GUI or text interface. The most likely cause of a `signal 11 error` during installation is a hardware error related to memory or the cache associated with the CPU (micro-processor).

![](img/9f89727199836b0f871f1745838aa8b2_87_1.png)

`Signal 11`, also known as SIGSEGV (short for Segment Violation Signal), can occur in other Linux applications. A `segment violation` occurs when a process tries to access a memory location that it's not supposed to access. The operating system catches the problem before it happens and stops the offending process by sending it a signal 11. When that happens during installation, it means `anaconda` made an error while accessing memory, and the most likely reason is some hardware problem. A commonly suggested cure for the signal 11 problem is to turn off the CPU cache in the BIOS. To do so, you have to enter SETUP while the PC boots (by pressing a function key such as F2) and then turn off the CPU cache from the BIOS setup menus.

If the problem is due to a hardware error in memory (in other words, the result of bad memory chips), you could try swapping the memory modules around in their slots. You may also consider replacing an existing memory module with another memory module, if you have one handy.

You can read more about the signal 11 problem at `www.bitwizard.nl/sig11/`.

## Using kernel boot commands

When you boot the PC for installation, either from the DVD or the first CD-ROM, you get a text screen with the `boot:` prompt. Typically, you press Enter at that prompt or do nothing and the installation begins shortly. You can, however, type quite a variety of commands at the boot prompt. The commands can provide options to the Linux kernel that takes care of the installation and controls various aspects of the installation such as whether the kernel should probe for hardware or whether to use GUI screens for the installation. Some of these commands can be helpful in bypassing problems that you may encounter during installation.

To use these boot commands, type **linux** followed by the boot command. For example, to perform text-mode installation and tell the kernel that your PC has 256MB of memory, you type the following at the boot prompt:

```
linux text mem=256M
```

Consult Table 3-1 for a brief summary of some of the Linux boot commands. You can use these commands to turn certain features on or off.

Although I mention these Linux kernel boot commands in the context of troubleshooting installation problems, you can use many of these commands any time you boot a PC with any Linux distribution and you want to turn specific features on or off.

![](img/9f89727199836b0f871f1745838aa8b2_88_0.png)

### Table 3-1 Some Common Linux Kernel Boot Commands

| Command | Description |
| :--- | :--- |
| `askmethod` | Prompts you for other installation methods such as installing over the network using NFS, FTP, or HTTP. |
| `apic` | Works around a bug commonly encountered in the Intel 440GX chipset BIOS and only executes with the installation program kernel. |
| `acpi=off` | Disables ACPI (Advanced Configuration and Power Interface) in case there are problems with ACPI. |
| `dd` | Prompts for a driver disk during the installation of Red Hat Linux. |
| `display=IP_address:0` | Causes installer GUI to appear on the remote system identified by the IP address. (Make sure that you run the command `xhost +hostname` on the remote system where `hostname` is the host where you are running the installer.) |
| `driverdisk` | Performs the same function as the `dd` command. |
| `enforcing=0` | Turns off Security Enhanced Linux (SELinux) mandatory access control. |
| `expert` | Enables you to partition removable media and prompts for a driver disk. |
| `ide=nodma` | Disables DMA (direct memory access) on all IDE devices and can be useful when you are having IDE-related problems. |
| `ks` | Configures the Ethernet card using DHCP and then runs a kickstart installation by using a kickstart file from an NFS server identified by the `bootServer` parameters provided by the DHCP server. |
| `ks=kickstartfile` | Runs a kickstart installation by using the kickstart file specified by `kickstartfile`. (The idea behind kickstart is to create a text file with all the installation options and then “kick start” the installation by booting and then providing the kickstart file as input.) |
| `lowres` | Forces the installer GUI to run at a lower resolution (640x480). |
| `mediacheck` | Prompts you if you want to check the integrity of the CD image (also called the ISO image). Checking the image is done by computing the MD5 *checksum* and comparing that with the official Fedora Core value. It can take a few minutes to check a CD-ROM. |
| `mem=xxxM` | Overrides the amount of memory the kernel detects in the PC (some older machines could detect only 16MB of memory, and on some new machines the video card may use a portion of the main memory). Replace xxx with the number representing the megabytes of memory in your PC. |
| `nmi_watchdog=1` | Enables the built-in kernel deadlock detector that makes use of Non Maskable Interrupt (NMI). |
| `noapic` | Prevents the kernel from using the Advanced Programmable Interrupt Controller (APIC) chip. (Use this command on motherboards known to have a bad APIC.) |
| `nofirewire` | Does not load support for FireWire. |
| `noht` | Disables *hyperthreading* (a feature that enables a single processor to act as multiple virtual processors at the hardware level). |
| `nomce` | Disables self-diagnostics checks performed on the CPU by using Machine Check Exception (MCE). On some machines, these checks are performed too often and need to be disabled. |
| `nomount` | Does not automatically mount any installed Linux partitions in rescue mode. |
| `nopass` | Does not pass the keyboard and mouse information to stage 2 of the installation program. |
| `nopcmcia` | Ignores any PCMCIA controllers in system. |
| `noprobe` | Disables automatic hardware detection and instead prompts the user for information about SCSI and network hardware installed on the PC. You can pass parameters to modules by using this approach. |
| `noshell` | Disables shell access on virtual console 2 (the one you get by pressing Ctrl+Alt+F2) during installation. |
| `nousb` | Disables the loading of USB support during the installation (may be useful if the installation program hangs early in the process). |
| `nousbstorage` | Disables the loading of the usbstorage module in the installation program's loader. It may help with device ordering on SCSI systems. |
| `reboot=b` | Changes the way the kernel tries to reboot the PC so that it can reboot even if the kernel hangs during system shutdown. |
| `pci=noacpi` | Causes the kernel to not use ACPI to route interrupt requests (IRQs). |
| `rescue` | Starts the kernel in rescue mode where you get a shell prompt and can try to fix problems. |
| `resolution=HHHxVVV` | Causes the installer GUI to run in the specified video mode (replace $HHH$ and $VVV$ with standard resolution numbers, such as 640x480, 800x600, 1024x768, and so on). |
| `selinux=0` | Disables the SELinux kernel extensions. |
| `serial` | Turns on serial console support during installation. |
| `skipddc` | Skips the Display Data Channel (DDC) probe of monitors (useful if the probing causes problems). |
| `text` | Runs the installation program in text mode. |

# Setting Up Printers

The Fedora Core installer does not include a printer configuration step, but you can easily configure a printer from a graphical utility program. To set up printers, follow these steps:

- 1. **From the graphical login screen, log in as root.**
    If you're not logged in as `root`, proceed to the next step and the printer configuration tool prompts you for the `root` password.
