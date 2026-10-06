
16. Which program is used by the installation procedure to configure X?

- A. Xconfig
- B. Xconfigurator
- C. XF86Config
- D. XF86Setup

17. Which of the following is an appropriate response if you can't boot the installation procedure by using the system’s CD-ROM drive?

- A. Revise the BIOS settings to permit booting from CD-ROM.
- B. Install a memory upgrade.
- C. Boot from a boot floppy.
- D. Boot using autoboot.bat.

18. Why should you create a boot disk?

- A. Creating the boot disk proves Linux is properly installed.
- B. You can use it to boot your system.
- C. You can't boot the system from the hard drive until installation is complete.
- D. You can't create one after installation is complete.

## Answers to Review Questions

- 1. A, B, C. Upgrade is an installation type, not an installation mode.
- 2. A, B, C, and D. You can use a variety of techniques during a graphical mode installation.
- 3. A, B, B. You cannot use the mouse during a text mode installation.
- 4. B. Expert mode installation lets you avoid device probes that might hang the system.
- 5. A, B, C, D. Table 7.1 summarizes the installation program’s use of virtual consoles.
- 6. A, B, D. Partitioning may be performed automatically. Network configuration is performed only if a network adapter is present. Authentication configuration occurs only during Custom installations.
- 7. D. A three-button mouse is preferred for use with X. If you have a two-button mouse, you should generally enable three-button emulation.
- 8. B, C, D. There is no Expert installation class. Installation classes other than Custom are automatically formatted.
- 9. B. A mount point is a directory bound to a mounted device by the mount command.
- 10. D. When you enable the Grow to Fill, the installation program makes the partition as large as possible.
- 11. C. You should use the OS/2 boot manager to load Linux by fetching LILO from the boot partition.
- 12. C. A DHCP server can supply network configuration information to a system at boot time.
- 13. A. Another operating system may not support setting the system clock to UTC. Setting the clock to UTC has no effect on accuracy. The local time zone must be known to the system, so the time zone must be.
- 14. A, D. Specify an NIS domain or server only if you plan to use network passwords.
- 15. B. The Unresolved Dependencies screen tells you that additional packages may need to be installed.
- 16. B. The installation program uses Xconfigurator to configure X.
- 17. A, C, D. Many systems—especially older systems—cannot boot from a CD-ROM drive.
- 18. B. The boot disk is handy if your system’s boot information becomes damaged.

## Advanced Installations

RHCE PREPARATION TOPICS COVERED IN THIS CHAPTER:

- Understand how and be able to install Red Hat Linux on a compatible laptop computer.
- Understand how and be able to install Red Hat Linux in a multi-boot configuration.
- Understand how and be able to configure and troubleshoot the Linux loader, LILO.
- Understand how and be able to install Red Hat Linux on a computer that requires PCMCIA support during installation.
- Understand how and be able to install Red Hat Linux using a network server to provide access to installation media.
- Understand how and be able to perform an automated (kickstart) installation of Red Hat Linux.

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_196_0.png)

This chapter covers some odds and ends related to installation. It explains how to cope with several unusual facilities of installations, how to configure and troubleshoot several Linux facilities, and how to perform installations by using network servers. Although some of these topics seem to be of minor importance, examination questions are apt to address these topics. Be sure you invest sufficient time to master this chapter, paying special attention to unfamiliar topics.

## Installing Linux on Laptops

Installing Linux on a laptop often presents complications. The biggest obstacle is that laptop manufacturers generally do not standardize the components used in a model laptop. For example, laptops manufactured at one time or location may have a different sound card than units manufactured at another time or location. Thus, one laptop owner may have little difficulty installing Linux, but someone else who owns the same model laptop and follows the same installation procedure as the first owner may be unable to properly configure Linux. To further complicate matters, laptop technology advances at a more rapid pace than desktop technology. Manufacturers introduce new models every month.

A second obstacle is that laptops are more likely than desktop computers to use integrated components and chipsets that are not widely used. Linux drivers supporting such components and chipsets are sometimes unavailable. For example, many laptops use video hardware that is not supported by XFree86 or sound hardware that is not supported by the standard kernel and drivers. You may be able to employ a commercial server or sound card driver to support unusual hardware. For example, see Metro Link.

Laptops are more likely than desktop computers to use integrated components and chipsets that are not widely used. Linux drivers supporting such components and chipsets are sometimes unavailable. For example, many laptops use video hardware that is not supported by XFree86 or sound hardware that is not supported by the standard kernel and drivers. You may be able to employ a commercial server or sound card driver to support unusual hardware. For example, see Metro Link.

Laptops are more likely than desktop computers to use integrated components and chipsets that are not widely used. Linux drivers supporting such components and chipsets are sometimes unavailable. For example, many laptops use video hardware that is not supported by XFree86 or sound hardware that is not supported by the standard kernel and drivers. You may be able to employ a commercial server or sound card driver to support unusual hardware. For example, see Metro Link.

## Performing Multi-Boot Installations

Many Linux users want to use a single computer to host multiple systems in what is called multi-boot configuration. In a multi-boot configuration, each time you start the system, you choose the operating system you want to boot. However, instead of configuring a system for multi-boot operation, you can install special software that lets you use Windows programs. For example, the WINE project (www.winehq.com) is implementing the Win32 API under Linux. Already, you can use WINE to run many Windows programs under Linux. Another approach to running Windows programs under Linux is VMware, Inc.'s product called VMware, which lets you run the Windows 9x or the Windows operating system under Linux. Alternatively, a Windows NT version of VMware lets you Linux under Windows NT. The company's website is www.vmware.com. One of the most useful features of VMware is its ability to run multiple versions of Linux on a single computer. By doing so, you can install, configure, and test new versions of Linux without disturbing a running server.
