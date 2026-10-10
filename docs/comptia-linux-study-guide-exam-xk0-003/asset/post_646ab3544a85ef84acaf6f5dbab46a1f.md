
## Summary

Before installing Linux, you should take some time to plan the implementation. This begins with determining which Linux distribution to use, and it continues with planning what installation media you want to use.

After installing Linux, you may need to attend to certain details. One of these is boot loader configuration. Although the installer usually gets this detail correct, particularly for single-OS systems, you may want to tweak the settings or add other OSs to the boot loader. You’ll also need to understand this process when you install a new kernel down the road. In case you have problems booting your system, you should know how to troubleshoot boot problems by entering single-user mode, examining **dmesg** output, and using rescue discs.

Another common post-installation configuration detail is getting X working. Again, Linux distributions usually configure X correctly during installation, but you may need to tweak the settings or change them at a later date.

Finally, certain hardware management tools are vital to Linux administrators. You must be able to locate compatible hardware, identify the hardware you have installed, and configure it.

## Exam Essentials

**Summarize the concept of a Linux distribution.** A distribution is a collection of software developed by diverse individuals and groups, bound by an installation routine. Linux distributions can differ in many details, but they all share the same heritage and the ability to run the same programs.

**Describe when it’s most appropriate to use CD-ROM and network installations.** CD-ROM installations are most convenient when installing to systems with poor network connectivity or when you have a CD-ROM and want to install quickly. Network installations are convenient when you are installing several systems simultaneously or when you don’t have a Linux CD-ROM or a CD-ROM drive on the target system.

**Summarize the x86 boot process.** The CPU executes code stored on the BIOS, which redirects the CPU to load and execute a boot loader from the MBR. This boot loader may load the OS kernel or redirect the boot process to another boot loader, which in turn loads the kernel and starts the OS running.

**Explain the purpose of single-user mode.** In single-user mode, Linux runs without most of the background processes or support for multiuser logins that are hallmarks of a normal Linux boot. Relieving the system of these processes enables you to perform low-level maintenance tasks that might not otherwise be possible.

**Describe why you might use an emergency disc.** An emergency disc enables you to boot a computer into Linux even when the Linux system installed on the computer is too badly damaged to boot. You can then use the disc-based system to perform data recovery or reconfigure the system on the hard disk.

**Determine what video chipset your system uses.** Many manufacturers document the video card chipset in their manuals or on the product boxes. You can also check the Microsoft Windows System Control Panel, if the manufacturer did not make the information readily available.

**Summarize how X determines the monitor's refresh rate.** X uses the monitor's maximum horizontal and vertical refresh rates and a series of fixed mode lines, which define particular timings for various video resolutions. X picks the mode line that produces the highest refresh rate supported by the monitor at the specified resolution.

**Explain the purpose of an XDMCP server.** XDM, KDM, and GDM are the three main Linux XDMCP servers. Each of them enables users to log into the system with X running, thus bypassing the text-mode login that many users find off-putting.

**Summarize some tools for identifying hardware in Linux.** The `lspci` and `lsusb` commands display information on PCI and USB hardware, respectively. The `lsmod` command displays the kernel driver modules that are loaded. The `/proc` filesystem is a treasure trove of hardware information, although many of its files contain highly technical information that can be difficult to interpret.

## Review Questions

1. In what ways do Linux distributions differ from one another? (Choose all that apply.)
   - **A.** Package management systems
   - **B.** Kernel development history
   - **C.** Installation routines
   - **D.** The ability to run popular Unix servers

2. Which of the following best describes a typical Linux distribution's method of installation?
   - **A.** The installation program is a small Linux system that boots from floppy, CD-ROM, or hard disk to install a larger system on the hard disk.
   - **B.** The installation program is a set of DOS scripts that copies files to the hard disk, followed by a conversion program that turns the target partition into a Linux partition.
   - **C.** The installation program boots only from a network boot server to enable installation from CD-ROM or network connections.
   - **D.** The installation program runs under the Minix OS, which is small enough to fit on a floppy disk but can copy data to a Linux partition.

3. Which of the following is an advantage of a GUI installation over a text-based installation?
   - **A.** GUI installers support more hardware than do their text-based counterparts.
   - **B.** GUI installers can provide graphical representations of partition sizes, package browsers, and so on.
   - **C.** GUI installers can work even on video cards that support only VGA graphics.
   - **D.** GUI installers better test the system's hardware during the installation.

4. What is an advantage of a network installation over a DVD-ROM installation from a downloaded image file?
   - **A.** A network installation can result in less material downloaded.
   - **B.** A network installation will proceed more quickly once started.
   - **C.** A network installation will result in fewer disc swaps.
   - **D.** A network installation will work even if there's a DHCP error.

5. Where might the BIOS find a boot loader?
   - **A.** RAM
   - **B.** `/dev/boot`
   - **C.** MBR
   - **D.** `/dev/kmem`

6. Which command is used to install GRUB into the MBR of your first ATA hard drive?
   - A. grub (hd0,1)
   - B. grub-install /dev/hda1
   - C. lilo /dev/hda
   - D. grub-install /dev/hda

7. Which of the following files might you edit to configure GRUB? (Choose all that apply.)
   - A. /boot/grub/menu.lst
   - B. /etc/grub.conf
   - C. /boot/grub/grub.conf
   - D. /boot/menu.conf

8. The string root (hd1,5) appears in your /boot/grub/menu.lst file. What does this mean?
   - A. GRUB tells the kernel that its root partition is the fifth partition of the first disk.
   - B. GRUB looks for files on the sixth partition of the second disk.
   - C. GRUB looks for files on the fifth partition of the first disk.
   - D. GRUB installs itself in /dev/hd1,5.

9. What string would you add to the end of a GRUB kernel line to boot into single-user mode? (Choose all that apply.)
   - A. 1
   - B. single
   - C. emerg
   - D. one

10. You want to examine the kernel ring buffer to debug a hardware problem. How would you do this?
    - A. Type ringbuffer at a command prompt.
    - B. Type dmesg at a command prompt.
    - C. Reboot and add the string ring to the kernel line in GRUB.
    - D. Install a Token Ring device and examine its output.

11. What is an advantage of using an emergency disc versus using single-user mode?
    - A. An emergency disc may work even if Linux won't boot into single-user mode.
    - B. An emergency disc may work even if you've lost the root password.
    - C. An emergency disc may work even if multiple users are logged in.
    - D. An emergency disc may work even if the CPU is defective.

12. To reset a root password that you’ve forgotten, you blank the second field in root’s entry in `/etc/shadow`. What should you do then?
    - A. Copy `/etc/shadow` so that you don’t forget the password again.
    - B. Type `shadow-update` to update the shadow passwords.
    - C. Delete the entry for `root` in `/etc/passwd`.
    - D. Use `passwd` to set a new password for `root`.

13. Which of the following is the *most* useful information in locating an X driver for a video card?
    - A. The interrupt used by the video card under Microsoft Windows
    - B. The name of the driver used by the card under Microsoft Windows
    - C. Whether the card uses the ISA, VLB, PCI, or AGP bus
    - D. The name of the video card’s manufacturer

14. Which of the following summarizes the organization of the `xorg.conf` file?
    - A. The file contains multiple sections, one for each screen. Each section includes subsections for individual components (keyboard, video card, and so on).
    - B. Configuration options are entered in any order desired. Options relating to specific components (keyboard, video card, and so on) may be interspersed.
    - C. The file begins with a summary of individual screens. Configuration options are preceded by a code word indicating the screen to which they apply.
    - D. The file is broken into sections, one or more for each component (keyboard, video card, and so on). The end of the file has one or more sections that define how to combine the main sections.

15. In what section of `xorg.conf` do you specify the resolution that you want to run?
    - A. In the `Screen` section, subsection `Display`, using the `Modes` option
    - B. In the `Monitor` section, using the `Modeline` option
    - C. In the `Device` section, using the `Modeline` option
    - D. In the `DefaultResolution` section, using the `Define` option

16. Which of the following features do KDM and GDM provide that XDM doesn’t?
    - A. An encrypted remote X-based access ability, improving network security
    - B. The ability to accept logins from remote computers, once properly configured
    - C. The ability to select the login environment from a menu on the main login screen
    - D. A login screen that shows the username and password simultaneously rather than sequentially
