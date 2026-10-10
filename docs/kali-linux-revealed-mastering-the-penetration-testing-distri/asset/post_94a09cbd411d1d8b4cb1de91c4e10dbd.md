
In the Storage screen (Figure 2.14, “Storage Settings” [page 33]), you should associate the Kali Linux ISO image with the virtual CD/DVD-ROM reader. First, select the CD-ROM drive in the Storage Tree list and then click on the small CD-ROM icon on the right to display a contextual menu where you can Choose Virtual Optical Disk File...

![](img/46e3313ea1bb2892f314630a4f0677b8_60_0.png)

Figure 2.15 System Settings: Motherboard

In the System screen (Figure 2.15, “System Settings: Motherboard” [page 34]), you will find a Motherboard tab. Make sure that the boot order indicates that the system will first try to boot from any optical device before trying a hard disk. This is also the tab where you can alter the amount of memory allocated to the virtual machine, should the need arise.

![](img/46e3313ea1bb2892f314630a4f0677b8_61_0.png)

**Figure 2.16**  System Settings: Processor

In the same screen but on the “Processor” tab (Figure 2.16, “System Settings: Processor” [page 35]), you can adjust the number of processors assigned to the virtual machine. Most importantly, if you use a 32-bit image, enable PAE/NX or the Kali image will not boot since the default kernel variant used by Kali for i386 (aptly named “686-pae”) is compiled in a way that requires Physical Address Extension (PAE) support in the CPU.

There are many other parameters that can be configured, like the network setup (defining how the traffic on the network card is handled), but the above changes are sufficient to be able to boot a working Kali Linux live system. Finally, click Boot and the VM should boot properly, as shown in Figure 2.17, “Kali Linux Boot Screen in VirtualBox” [page 36]. If not, carefully review all settings and try again.

![](img/46e3313ea1bb2892f314630a4f0677b8_62_0.png)

**Figure 2.17** *Kali Linux Boot Screen in VirtualBox*

## VMware

*VMware Workstation Pro* is very similar to *VirtualBox* in terms of features and user interface, because they are both designed primarily for desktop usage, but the setup process for a new virtual machine is a bit different.

![](img/46e3313ea1bb2892f314630a4f0677b8_63_0.png)

The initial screen, shown in Figure 2.18, “VMware Start Screen” [page 37], displays a big Create a New Virtual Machine button that starts a wizard to guide you through the creation of your virtual machine.

![](img/46e3313ea1bb2892f314630a4f0677b8_63_1.png)

In the first step, you must decide whether you want to be presented with advanced settings during the setup process. In this example, there are no special requirements so choose the typical installation, as shown in Figure 2.19, “New virtual Machine Wizard” [page 37].

![](img/46e3313ea1bb2892f314630a4f0677b8_64_0.png)

Figure 2.20 Guest Operating System Installation

The wizard assumes that you want to install the operating system immediately and asks you to select the ISO image containing the installation program (Figure 2.20, “Guest Operating System Installation” [page 38]). Select “Installer disc image file (iso)” and click on Browse to select the image file.

![](img/46e3313ea1bb2892f314630a4f0677b8_64_1.png)

Figure 2.21 Select a Guest Operating System

When the operating system (OS) cannot be detected from the selected ISO image, the wizard asks you which guest OS type you intend to run. You should select “Linux” for the OS and “Debian 8.x” for the version, as shown in Figure 2.21, “Select a Guest Operating System” [page 38].

![](img/46e3313ea1bb2892f314630a4f0677b8_65_0.png)

Choose “Kali Linux” as the name of the new virtual machine (Figure 2.22, “Name the Virtual Machine” [page 39]). As with VirtualBox, you also have the option to store the VM files in an alternate location.

![](img/46e3313ea1bb2892f314630a4f0677b8_66_0.png)

Figure 2.23 Specify Disk Capacity

The default hard disk size of 20 GB (Figure 2.23, “Specify Disk Capacity” [page 40]) is usually sufficient but you can adjust it here depending on your expected needs. As opposed to VirtualBox, which can use a single file of varying size, VMware has the ability to store the disk’s content over multiple files. In both cases, the goal is to conserve the host’s disk space.

![](img/46e3313ea1bb2892f314630a4f0677b8_67_0.png)

*Figure 2.24 Ready to Create Virtual Machine*

VMware Workstation is now configured to create the new virtual machine. It displays a summary of the choices made so that you can double-check everything before creating the machine. Notice that the wizard opted to allocate only 512 MB of RAM to the virtual machine, which is not enough so click on Customize Hardware... (Figure 2.24, “Ready to Create Virtual Machine” [page 41]) and tweak the Memory setting, as shown in Figure 2.25, “Configure Hardware Window” [page 42].

![](img/46e3313ea1bb2892f314630a4f0677b8_68_0.png)

After a last click on Finish (Figure 2.24, “Ready to Create Virtual Machine” [page 41]), the virtual machine is now configured and can be started by clicking “Power on this virtual machine” as shown in Figure 2.26, “Kali Linux Virtual Machine Ready” [page 43].

![](img/46e3313ea1bb2892f314630a4f0677b8_69_0.png)

Figure 2.26 Kali Linux Virtual Machine Ready

## 2.3. Summary

In this chapter, you learned about the various Kali Linux ISO images, learned how to verify and download them, and learned how to create bootable USB disks from them on various operating systems. We also discussed how to boot the USB disks and reviewed how to configure the BIOS and startup settings on various hardware platforms so that the USB disks will boot.

Summary Tips:

- www.kali.org is the only official download site for Kali ISOs. Do not download them from any other site, because those downloads could contain malware.
- Always validate the sha256sum of your downloads with the sha256sum command to ensure the integrity of your ISO download. If it doesn’t match, try the download again or use a different source.
- You must write the Kali Linux ISO image to a bootable media if you want to boot it on a physical machine. Use Win32 Disk Imager on Windows, the Disks utility on Linux, or the dd command on Mac OS X/macOS. Be very careful when writing the image. Selecting the wrong disk could permanently damage data on your machine.
- Configure the BIOS/UEFI setup screens on a PC or hold the Option key on OS X/macOS to allow the machine to boot from the USB drive.
- Virtual machine programs like *VirtualBox* and *VMware Workstation Pro* are especially useful if you want to try out Kali Linux but aren't ready to commit to installing it permanently on your machine or if you have a powerful system and want to run multiple operating systems simultaneously.

Now that you have a working installation of Kali Linux, it is time to delve into some Linux fundamentals that are required for basic and advanced operation of Kali. If you are a moderate to advanced Linux user, consider skimming the next chapter.

![](img/46e3313ea1bb2892f314630a4f0677b8_71_0.png)

## Keywords

- Linux kernel
- User space
- Command line
- bash
- Filesystem Hierarchy
- Unix commands

![](img/46e3313ea1bb2892f314630a4f0677b8_72_0.png)

# 3 Linux Fundamentals

Contents

- What Is Linux and What Is It Doing? 48
- The Command Line 51
- Useful Commands 56
- The File System 54
- Summary 62

Before you can master Kali Linux, you must be at ease with a generic Linux system. Linux proficiency will serve you well, because a large percentage of web, email, and other Internet services run on Linux servers.

In this section, we strive to cover the basics of Linux, but we assume that you already know about computer systems in general, including components such as the CPU, RAM, motherboard, and hard disk, as well as device controllers and their associated connectors.

### 3.1. What Is Linux and What Is It Doing?

The term "Linux" is often used to refer to the entire operating system, but in reality, Linux is the operating system kernel, which is started by the boot loader, which is itself started by the BIOS/UEFI. The kernel assumes a role similar to that of a conductor in an orchestra—it ensures coordination between hardware and software. This role includes managing hardware, processes, users, permissions, and the file system. The kernel provides a common base to all other programs on the system and typically runs in *ring zero*, also known as *kernel space*.

**The User Space**  We use the term *user space* to lump together everything that happens outside of the kernel.

Among the programs running in user space are many core utilities from the GNU project[1], most of which are meant to be run from the command line. You can use them in scripts to automate many tasks. Refer to section 3.4, "Useful Commands" [page 56] for more information about the most important commands.

Let's quickly review the various tasks handled by the Linux kernel.

### 3.1.1. Driving Hardware

The kernel is tasked, first and foremost, with controlling the computer's hardware components. It detects and configures them when the computer powers on, or when a device is inserted or re- moved (for example, a USB device). It also makes them available to higher-level software, through a simplified programming interface, so applications can take advantage of devices without having to address details such as which extension slot an option board is plugged into. The programming interface also provides an abstraction layer; this allows video-conferencing software, for exam- ple, to use a webcam regardless of its maker and model. The software can use the *Video for Linux (V4L)* interface and the kernel will translate function calls of the interface into actual hardware commands needed by the specific webcam in use.

The kernel exports data about detected hardware through the `/proc/` and `/sys/` virtual file sys- tems. Applications often access devices by way of files created within `/dev/`. Specific files rep-

[1] http://www.gnu.org
