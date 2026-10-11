
PCI Configuration Note

- Note the difference in spelling between the second and third set of options – about all that **APCI** and **APIC** have in common is the letters in their names. Press **F10** to boot with the options you added. Once you find a combination that has the kernel and your hardware co-existing with one another, make the change permanent by adding the options to `GRUB_CMDLINE_LINUX_DEFAULT` and `GRUB_CMDLINE_LINUX` in `/etc/default/grub`, saving the file and updating Grub with one of these commands. Which one depends on your distro – if the first one fails, try the second and then the third.

```bash
sudo update-grub2
sudo grub2-mkconfig -o /boot/grub2/grub.cfg
sudo grub2-mkconfig -o /boot/grub/grub.cfg
```

## Re-installing Windows broke Linux

I installed Linux on my Windows computer and it gave me the choice of which to use when I turned it on. I recently had to reinstall Windows and now Linux has disappeared. I don't want to reinstall Linux as I would lose all my documents and settings. Is there any way to get my Linux back?

Linux uses the Grub bootloader to choose between different boot options, but Windows uses its own bootloader. A bootloader is a small piece of code embedded at the start of your hard drive that kickstarts the process of loading your operating system. When you installed Windows, it installed its own bootloader, overwriting your existing Grub. Don't worry, it's only the bootloader code that's gone – your Linux system and files are still there, and all you need to do is restore Grub. Some distro install discs have an option to repair the bootloader, or there's a more generic option in Rescatux (www.supergrubdisk.org/rescatux). Boot from the Rescatux CD and select the Restore Grub option. This will search for your Linux partitions and ask you to choose the partition that contains the root filesystem of your Linux installation and then ask which hard disk you want to install Grub on – usually /dev/sda, the first disk. The window may go blank for a worrying amount of time but do not panic or reboot: wait until it tells you Grub was re-installed before rebooting, and you should then get your old boot menu back, with access to your untouched Linux system.

## Dual-booting more than one distro

I know I can dual-boot between Linux and Windows, but can I do the same with more than one Linux distro? If so, how do I share my data between them?

### How should I partition my disk?

Yes, it is possible. Each distro needs its own **root** partition but you can share the same **swap** between them all. Having a separate partition for /home is recommended – you don't want to tie your data to a single distro you may later decide to stop using. While a separate /home partition is desirable, don't use the same **home** directory for each distro as there may be incompatibilities between different versions of the software used. I prefer to put the distro name in the username, as in “fred-ubuntu”, “fred-debian”, etc. As long as each user has the same UID – most installers make the first user 1000 – you'll have write access to all of them, then you can create symlinks for important data directories, like documents, music, photos and so on, to share these files between all distros while keeping the configuration files separate.

As far as the boot menu is concerned, pick one distro as your main one and let that handle booting. Every time you install a new distro, skip the option to install a bootloader if possible. Then reboot into the main one and run:

```bash
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

- To make permanent changes to your Grub menu, edit `/etc/default/grub` and run `grub2-mkconfig` or `update-grub`.

## Removing a distro broke everything

I deleted Linux partitions from my computer, in preparation for installing something else. Now I cannot boot it. All I get is a message that Grub cannot find files and a prompt saying 'grub rescue>' I can't even boot the Windows.

While the initial boot code for Grub is stored in the **Master Boot Record** (MBR) at the start of your hard disk, this is a very small space. So the initial Grub code loads files and configuration information from the `grub` or `grub2` directory on your Linux boot partition. When you removed that partition, you left Grub nowhere to go. If you are planning on installing another distro in the now-empty space, simply run the installer and it will set up Grub for you, detecting your Windows system too, and all will be well after a reboot.

If you are using the space for an existing Windows or Linux installation, you need to either set up Grub for the other Linux system or reinstall the Windows bootloader. The easiest way to reset Grub is use the Restore Grub option on the **Rescatux** live CD – choose the Linux installation you want to be responsible for holding the Grub files. Restoring the Windows bootloader involves booting the Windows disc (or rescue partition) and running one of these commands, depending on the Windows version. For Windows XP it's the following:

```bash
fixboot
fixmbr
```

For Vista and Windows 7 and 8 it's:

```bash
bootrec /fixboot
bootrec /fixmbr
bootrec /rebuildbcd
```

When your computer won't even boot, a live CD is a godsend, so it pays to always have one handy. A live CD is a complete Linux environment that boots from a CD and needs no installation. Apart from being very handy, a live CD is ideal for a rescue system. There are some dedicated rescue CDs, such as System Rescue CD, Rescatux and Gnil, but most distro installer discs nowadays boot into a live environment that contains enough software to fix many problems.

## Hardware difficulties

Solving problems with recalcitrant bits of kit.

![](img/420a7272a6efa239082a35eeadd9bc1d_127_0.png)

### Finding hardware drivers

**Q** Where do I get drivers for my hardware?

**Q** The accompanying disc includes Windows drivers only.

**A** Most hardware doesn’t need separate drivers with Linux; the kernel includes drivers for a massive range of hardware. Nine times out of ten, the kernel recognises the hardware when you plug it in and loads the appropriate driver without any input from you. Some hardware does have separate drivers, often because they use proprietary code that cannot be included with the kernel. In such cases, a live CD, such as Knoppix or System Rescue CD, will often recognise the device – these tend to include a lot of extra drivers. If the hardware is an internal device, it will usually show up in the output from **lspci**, and adding the **-k** option shows which driver is being used.

Once you know that, you can search for which package provides that driver, either using your package manager or a web search. If it’s in a standard package that’s not installed by default, as is the case with many wireless drivers, installing the package should be all you need to get the hardware working. The process is similar with USB devices except you use the **lsusb** command, and there is no handy **-k** equivalent. Note that on some systems, these can only be run as root. If there’s no driver support by your kernel or package manager, you have to enter the murky waters of downloading and installing drivers directly from a manufacturer’s website. If they provide a **Deb** or **RPM** package suitable for your system, this isn’t too bad. Otherwise, make sure you get the right driver for your architecture and follow the installation instructions carefully. Drivers have to be linked into the kernel, so you will probably need the kernel source and build-essential packages installed.

### Random crashes

**Q** My computer is suffering from random crashes and lockups – it doesn’t seem to be related to any particular piece of software.

**A** This may well be a hardware issue and there are a number of common causes. Faulty memory can cause this and, because of the way **Linux** makes use of all available memory, it is more likely to do so in **Linux** than **Windows**. Install **Memtester** from the terminal with **sudo apt-get install memtester**. Let this run for at least a couple of passes, preferably overnight. Overheating is also a common cause: try running a system monitor or **Taskbar** applet that shows your system temperature. Make sure all vents are clear and, if you are comfortable with taking a screwdriver to your case, check that your **CPU** heatsink and fan are not clogged.

A third cause, for desktop computers, is a substandard power supply. Cheap units can often fail gradually, giving just this sort of behavior and damaging other components on their way down. The only reliable test is to try a different **PSU**.

### Printer problems

**Q** My distribution hasn’t spotted my printer. How do I install the drivers?

**A** How you install drivers – or even if there are any available – depends on your printer. The first place to go is [http://linuxprinting.org](http://linuxprinting.org) to check their database. If you do this before buying a printer, it will save you a lot of trouble. Enter the make and model of printer and their database will tell you if it is supported, and which drivers to use. **CUPS**, the printing system used by **Linux**, comes with many drivers, so there’s often no need to install anything.

![](img/420a7272a6efa239082a35eeadd9bc1d_127_1.png)

> While most distributions have a GUI for managing printers, the CUPS user interface is universal and works well.

### Why use the terminal?

Much of the advice we give here is in the form of terminal commands. While most distros have their own configuration programs, they vary considerably while the underlying commands they call remain constant across all distros. By cutting out the middle man and running those commands directly, the solutions we give are portable across all distros. It also means they work even if your problem is preventing the desktop from running.

Some commands need to be run as the root user, which is done either by prefixing the command with **sudo** (when you will be prompted to give your password) or by running **su** in the terminal first, which will ask you for the root password. We encourage you to use the sudo method throughout this article, as it is the only option with some distros. If you have full root access through **su**, simply run the command without **sudo**. Commands given without **sudo** should be run as your normal user.
