
# Installing Packages

Finally, the installation program will present the About to Install screen. The graphical mode version of this screen is shown in Figure 7.21. Up to this point, the configuration changes that you specified have been stored in RAM memory. You can reboot at this point without affecting the configuration of the target system. However, clicking Next commits the changes.

FIGURE 7.21 The About to install screen

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_183_0.png)

When you click Next, the installation program displays the Installing Packages screen. The graphical mode version of this screen is shown as Figure 7.22.

# Chapter 7 · Installing Red Hat Linux

# FIGURE 7.22 The Installing Packages screen

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_184_0.png)

The Installing Packages screen lets you monitor the progress of package installation. The Next button is disabled until the package installation is complete.

# Creating a Boot Disk

Unless you specified that no boot disk is needed, the installation program will display the Boot Disk Creation screen. The graphical version of this screen is shown in Figure 7.23.

# FIGURE 7.23 The Boot Disk Creation screen

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_185_0.png)

You can skip creation of the boot floppy disk by clicking Skip Boot Disk Creation and then clicking Next. However, in most cases, you should not do this; the boot disk is useful if you find that you're unable to boot Linux from the hard drive. To create the boot diskette, place a blank floppy disk in the floppy drive, and click Next.

# Completing the Installation

Next, the installation program will display the Congratulations screen, which signals the completion of installation. The graphical version of this screen is shown in Figure 7.24.

# 164 Chapter 7 · Installing Red Hat Linux

# FIGURE 7.24 The Congratulations screen

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_186_0.png)

You should remove the boot disk—if you created one—from the floppy drive, and click Exit. The computer will automatically restart. However, you may need to set your system's BIOS so that the system will boot from your hard disk. Now, practice installing Red Hat Linux by completing Exercise 7.1.

# EXERCISE 7.1

# Installing Red Hat Linux

Perform the following installations, exercising a variety of options so that you can see what they do:

- A graphical mode installation of a GNOME workstation
- A text mode installation of a server
- A graphical mode Custom installation
- An expert mode installation

When you're done with each installation, examine the installation log and become familiar with its typical contents. Knowing how the log should look will help you spot problems with actual installations.

# Summary

In this chapter, you learned how to install Red Hat Linux. The important topics covered are:

**Installation Modes** You can install Linux using graphical, text, or expert mode.

**Virtual Consoles** You can use Linux virtual consoles to monitor the installation procedure.

**Sequence of Operations** Several steps of the installation procedure are optional. They may be skipped based on user input, detected hardware, and detected installation media.

**Installation Path** The installation path defines the installation type and class.

**Partitioning** Hard disks can be partitioned automatically or manually.

**Network Configuration** By configuring the system to use a DHCP server (when available), network configuration can be automatically performed at boot time.

**Selecting Packages** You can select packages by component. You can also select individual packages. The GNOME Workstation, KDE Workstation, and Server installation classes automatically choose packages for you.

**X Configuration** The installation procedure can generally identify and automatically configure X for your video hardware. If you prefer, you can postpone configuring X.

**Boot Disk** You should generally create a boot disk, which is handy if your Linux system cannot be booted from the hard drive.

# Key Terms

Before sitting for the RHCE exam, be sure you're familiar with the following terms:

- components
- Custom installation class
- GNOME Workstation installation class
- installation path
- Install installation type
- KDE Workstation installation class
- package groups
- Server installation class
- three-button mouse emulation
- Upgrade installation type

# Additional Sources of Information

If you'd like further information about the topics presented in this chapter, you should consult the following sources:

- The Official Red Hat Linux Installation Guide
- The Official Red Hat Linux Getting Started Guide
- The Official Red Hat Linux Reference Guide

These documents are available on the Web, at www.redhat.com /support/manuals.

# Review Questions

1. Which of the following are Red Hat Linux installation modes?
A. Expert
B. Graphical
C. Text
D. Upgrade

2. Which of the following is true of graphical mode installation?
A. You can use the Tab key to select controls.
B. You can use the keyboard to enter text.
C. You can use the mouse to select an item from a list.
D. You can use the mouse to select controls.

3. Which of the following is true of text mode installation?
A. You can use the Tab key to select controls.
B. You can use the keyboard to enter text.
C. You can use the mouse to select an item from a list.
D. You can use the mouse to select controls.

4. What is the primary purpose of expert mode?
A. To impress colleagues and friends
B. To omit device
C. To specify boot parameters
D. To support network

5. Which of the following correctly pairs a virtual console with its installation function?
A. 1, install program
B. 2, shell prompt
C. 3, install messages
D. 4, kernel messages

6. Which of the following installation functions are optional?
- Partitioning
- Network configuration
- Setting the time zone
- Authentication configuration

7. Which of the following is true of a two-button mouse?
A. It is a bus mouse.
B. It is a PS/2 mouse.
C. It is a serial mouse.
D. You should generally enable three-button emulation.

8. Which installation is automatic performed for?
A. The GNOME Workstation class
B. The KDE Workstation class
C. The Server class

9. What is a mount point?
A. The device file associated with a removable device
B. The directory associated with a mountable device
C. The side of floppy diskette inserted into the drive
D. The time at which you insert the installation media

10. What should you do to make a partition as large as possible, given that other partitions have already been allocated?
A. Enter a big number as the size.
B. Enter a negative number as the size.
C. Enable the Allowable Type option.
D. Enable the Grow to Fill option.

11. If you plan to dual-boot OS/2 and Linux, where should you install LILO?
A. In memory
B. On CD-ROM
C. On the first sector of the Linux boot partition
D. On the master boot record

12. What happens when you configure the system to use DHCP?
A. Authentication is performed at boot time.
B. LILO installation is performed at boot time.
C. Network configuration is performed at boot time.
D. Partitioning is performed at boot time.

13. What will happen if you use the Time Zone screen to specify that the system clock be set to UTC?
A. A dual-boot operating system may malfunction.
B. Time will be kept more accurately.
C. Time will be kept somewhat less accurately.
D. You don't need to specify a time zone.

14. Which of the following authentication options should normally be set?
A. MD5 passwords
B. NIS domain
C. NIS server
D. Shadow passwords

15. When will the Unresolved Dependencies screen appear?
A. When disk geometry is unsuitable.
B. When packages you specify for installation require additional packages.
C. When you enter ambiguous information.
D. When you run low on system resources.
