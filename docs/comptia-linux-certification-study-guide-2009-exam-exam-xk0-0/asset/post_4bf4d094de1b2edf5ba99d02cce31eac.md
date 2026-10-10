
and modems). I was able to get the customer to print from the existing printers. How? I noticed on the HCL a printer mode that the existing 20 printers could emulate. This approach was used until the printer vendor was able to develop new printer drivers for the customer's new operating system. I miss the good old days!

The knowledge of the four-category approach for the most modern operating systems is a requirement for any computer professional. The Linux professional is no exception. Ironically, with the development of kernel-based architectures, many of today's operating systems hide a lot of their computer hardware functionality within the operating system. The Linux operating system does not. As a result, you should have a good understanding of how the Linux computer hardware works. For the Linux+ exam, you will need a fundamental understanding of the following components:

-   Power supplies are the devices required to provide the various computer hardware components [for example, motherboards and internal disk drives] within your system with direct current (DC). The power supply regulates the alternating current (AC) received from a wall's outlet by transferring it into DC required by computer chips; it is housed inside the system unit.

-   Motherboards are perforated circuit boards housed inside the system unit that contains the CPU, the memory (RAM) chips, and the slots available for the expansion cards. It is the largest printed circuit board; all the other expansion boards [for example, video cards and sound cards] interface with it to receive power and to provide bidirectional communications.

-   CPUs, the brains of the computer, are responsible for data processing and are the most important chip in the computer. CPUs control the functions performed by the various hardware components, processes all software instructions issued, and determines the speed of the system. The CPU is housed inside the system unit.

-   Memory, implemented as computer chips, helps process data or instructions by storing the instructions or data that the CPU processes.

-   Expansion boards are devices that expand the capabilities of a computer by enabling a range of different devices [for example, monitors, speakers, and modems] to communicate with the motherboard.

-   Video adapters are expansion cards that translate binary into the images viewed on the computer monitor.

-   Storage devices are internal and external devices (for example, hard disk drives, floppy disk drives, and CD drives) used for storing data and information.

> Note
>
> The Linux+ certification exam will not test you on computer hardware. However, it is important that you have a fundamental knowledge of the overall Linux Hardware Architecture.

For the Linux professional, the selection of which Linux distribution to use is dependent on the four hardware categories presented above. After selecting the desired Linux distribution, most distributions will allow you to install and configure your system hardware components during the installation phase. In addition, most distributions also support the installing, configuring, updating, and removing of hardware components after the system has been installed.

## EXERCISE 2.1: OpenSUSE Linux Hardware Compatibility List

In this exercise, we will review the Linux Hardware Compatibility List to determine whether openSUSE 11.1 can be installed on the Dell PowerEdge PE-T605 and HP Proliant DL380 G3 Servers. Complete the following:

1.  Open a **Web browser** from a workstation and navigate to http://en.opensuse.org/hardware.

2.  The compatible hardware can be viewed for full systems or individual components. Select the **Server category** underneath the Full Systems section. Is the Dell PowerEdge PE-T605 supported? Are there any installation problems listed?

3.  How about the HP Proliant DL380 G3?

## INSTALLING FROM LOCAL MEDIA

The Linux operating system’s successful installation is predicated upon good planning performed in advance. The purpose of this section is to present you with the major Linux installation decisions required during the operating system installation process. The decisions, presented within screenshots, will display the basic installation of the Linux operating system. The screenshots present the options you will face during the installation of the Linux operating system.

### Linux Installation Process

The Linux operating system can be installed from various different local [for example, CD, digital video disk (DVD), and iso images] and network [for example, File Transfer Protocol (FTP), Hyperext Transfer Protocol (HTTP), NFS, and Server Message Block (SMB) Server] sources. The *local media installation* method entails performing a stand-alone installation and does not rely on network connectivity to access to the installation source data. The *network source installation* method entails having an installation server available in your network or via an external server (for example, Internet) as the source where the installation data resides. Apart from a few unique settings, the installation process for each installation source is essentially the same. The “Installing across the Network” section presents the unique challenges associated with the installation of a Linux distribution from network sources. This section presents the installation of the Linux distribution from local media. Linux local media installation can be performed by using CD, DVD, or .iso sources. Of the choices provided, the author prefers .iso image installations.

As there are several Linux distributions available from various vendors and some are more popular than others, the first choice you face is the selection of a Linux distribution. The leading Linux distributions all follow the same installation stages. Gentoo is a notable exception. For this book, the authors have decided to use the openSUSE 11.1 Linux distribution. OpenSUSE 11.1 is the most current version available.

> Note
>
> The Linux+ certification exam is a vendor neutral exam. For a listing of the various Linux distributions, check out the following Web sites:
>
> - http://distrowatch.com/
> - http://en.wikipedia.org/wiki/List_of_Linux_distributions

## EXERCISE 2.2: Installing from Local Media

In this exercise, we will commence the initial installation of the openSUSE 11.1.1 installation using DVD Media. For this exercise, we will use the following:

1.  Open a **Web browser** from a workstation and navigate to http://software.opensuse.org/.
2.  Follow the instructions to download the openSUSE 11.1 DVD image.
3.  Create a bootable DVD from the .iso image using your burning software application.
4.  Boot the target machine with the newly created bootable network DVD.
5.  Select **Installation**. This will start the openSUSE Installer.

To launch the installation process from an .iso image, load the image as a CD/DVD into the virtualization software (for example, VMWARE workstation). Power up or reboot the virtual machine with the .iso image loaded to commence the initial boot process. The .iso image appeared as a DVD to the virtual machine. When the system completes the on-board self test, the openSUSE Installer program screen appears, as shown in Figure 2.2. The initial screen provides you with various menu options for installing openSUSE and additional configuration options required before the installation process. We will select the **Installation** option.

Below are descriptions of the choices:

-   **Boot from the hard disk** This option is used to automatically boot an existing Linux operating system (if previously installed on the hard disk). This prevents the automatic installation of a new Linux operating system.

### FIGURE 2.2

OpenSUSE Installer boot screen.

![](img/95b3ebd6248b36778ccf73988aaab2f2_28_0.png)

-   **Repair installed system** This option repairs a previously installed system. It boots the graphical repair system. This option also appears again after the System Probing phase covered later in the chapter.
-   **Installation** This option loads the mini Linux kernel from the Linux distribution and starts the installation process.
-   **Rescue System** This option starts a specialized small Linux kernel without a graphical user interface. It loads the Linux kernel into RAM and can modify configuration files, check the filesystem for defects, verify and/or modify the boot loader configuration, resize the partition, and a few other critical system modifications that may be necessary.
-   **Check installation media** To verify you have an authentic copy of Linux before installing, this option checks .iso image’s integrity. It uses the MD5 cryptographic hash algorithm. To verify the integrity of other media, a number of free MD5 and SHA cryptographic hash algorithms are available and downloadable from the Internet.
-   **Firmware test** This option tests the system’s Basic Input/Output System (BIOS) and Advanced Configuration and Power Interface (ACPI) compatibilities.
-   **Memory test** This option conducts systematic tests of your system RAM using memtest86. The memtest86 program is a stand-alone application for testing the physical memory on x86-based systems.

The remaining options located in the bar at the bottom of your screen are used as follows:

-   **F1 – Help** The Function 1 Key [F1] provides helpful information about the various options.
-   **F2 – Language** The key allows you to select a different language for the installation of Linux (The default language is English).
-   **F3 – Video mode** The key allows you to select a desired graphical [screen resolution] or text mode for installation.
-   **F4 – Source** This selection determines the Linux installation source [for example, FTP, HTTP, NFS, CD, DVD, SLP], as shown in Figure 2.3. The “Installing across the Network” section presents this option in greater detail. The default installation source selected is DVD.
-   **F5 – Kernel** The key allows you to disable potential hardware components [for example, ACPI systems and DMA modes].
-   **F6 – Driver** This key installs optional drivers or updates existing drivers.
