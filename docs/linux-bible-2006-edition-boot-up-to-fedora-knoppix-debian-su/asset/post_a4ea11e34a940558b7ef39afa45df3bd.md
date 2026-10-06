
# Installing Mac OS 9 or Below, Mac OS X, and Yellow Dog Linux on Multiple Drives

Because of the way system boots, you should have the drive to which you plan to install Yellow Dog Linux as the first hard drive in the IDE chain, set as Master. Mac OS or Mac OS X should be placed as the second drive in the chain and have the jumper set to Slave.

Then install the other versions of Mac OS (9 or below or X) onto the other hard drives. You only need to select a drive other than the first one during the install procedure. You must install Yellow Dog Linux as the last operating system and on the first drive.

# Yellow Dog Linux 3.0.1 Special Considerations

All the planning previously applies to Yellow Dog Linux 3.0.1, but there is one special consideration to take into account. Yellow Dog Linux 4.0.1 supports only New World systems, which are the blue-and-white G3 and above systems.

> Note: There are two versions of the G3, one has a beige case and that other has the blue-and-white case.

If you are installing Yellow Dog on a New World system, go to the next section, "Beginning the Installation."

If you are using an Old World system, which are beige G3 systems and below, refer to the Yellow Dog Linux Web site (http://www.yellowdoglinux.com) for information.

# Beginning the Installation

After you have determined how you will boot your system (multiboot or single Yellow Dog Linux boot) and have loaded Mac OS X or Mac OS 9 or below appropriate, you can begin installing Yellow Dog Linux. This procedure focuses on Yellow Dog 4.0.1, but special notes on 3.0.1 are included where appropriate.

- 1. Insert Yellow Dog CD 1 into your CD-ROM drive, reboot your system, and press C to boot off the CD-ROM.
- 2. If you downloaded Yellow Dog or have a burned CD-R, you may want to check your media by appending `mediacheck` to the end of any of the install types (see Step 3 for install types). For example:

```
install-safe mediacheck
```

This goes through all your media to determine if it is suitable for the operating system. This can save you a lot of time by determining that all of your CDs are good before you invest your time in the installation procedure.

# 372 Part III ♦ Choosing and Installing a Linux Distribution

Although it doesn't show up in the Yellow Dog 3.0.1 text menu, you can still type mediacheck after install or install-text to check your CD-ROMs.

- 3. After some curious probing messages, a menu asking how you want to boot the CD-ROM. If you are prompted with a New World ROM G3 or G4 system (blue-and-white machine), type install at the prompt to use the graphical user interface method of installation. If you are using a G5 machine, type install-g5 at the prompt to install using the graphical user interface.

If you can't get either of these methods to work, type install-safe for G3 or G4 machines or install-g5-safe for G5 machines to get a generic video mode for installation. If neither method works, you can type install for G3 or G4 machines or install-g5 for G5 machines to install the text installation method if you find the graphical version doesn't work for you.

Yellow Dog 3.0.1 has only install and install-text options available. Choose install, and if that doesn't work, choose install-text after rebooting.

- 4. The system will have been probed prior to this to determine the hardware configuration. After the text messages, you are presented with a welcome-screen. (You can choose to review the release notes by clicking the Release Notes button at the bottom-left side). When you're ready to move on, click the Next on the bottom-right side.

- 5. Select the language which you are most comfortable. All further information presented by the installer will be in the language you select.

- 6. Choose the keyboard that matches your current configuration.

- 7. Choose the type of installation you want. The options are:
- Personal Desktop—Most users will want this installation because it contains the most appropriate software set for home or office users (including laptops). Games, word processors, Internet tools, and other packages are included.
- Workstation—Similar to the personal desktop type but includes tools for system administration and software development.
- Server—Software needed for providing external services, including file and print, and mail services. This is an advanced installation type and should be used only if you need it because you could misconfigure your system and create a security vulnerability. You can install a graphical user interface as well, if you don't want the extra overhead of a GUI, you go without one on this type.
- Custom—Provides the most flexibility because you can configure the partitions and software packages you want (everything!). This is your choice if you want to have more control over the installation. If you want to experience a large set of applications, you can choose this instead of installing applications one by one. You can also choose a more specific set of packages if this is to be a server used for external services, providing a higher level of security.

For this chapter, the Custom installation type is used.

- 8. Decide how you want to partition your hard drive. You have two choices:

**Option 1: Automatically partitioning** — If you choose this method, click Next and you are presented with three options:

- **Remove Linux partitions on this system** — Deletes all previous Linux partitions and replaces previously identified Linux partitions.
- **Remove all partitions on this system** — Use this only on New World systems or on a single-boot system, it removes all previous installations, including any Mac OS or Mac X installation. If you use this on an old OS World system, regardless of the installation type, it destroys the installation and requires a format and reload of Mac OS.

Be extremely careful using the Remove All partitions. Avoiding it at all if possible you could accidentally destroy your Mac OS installation!

- **Keep all partitions and use existing space** — The one you want to use in most cases, it won't alter your Mac OS or Mac X installations and uses only the identified free space (as created previously). This is the option you select if you are using Automatically partitioning. You can also select the Review (and modify if needed) the partitions created, which will enable you to double-check the partitions that the installer creates for you and change them if needed.

**Option 2: Manually Partition with Disk Drill** — This is the more advanced option that allows you to create partitions to your preference. Here is the sequence for creating new Linux partitions:

- a. Choose the disk you want to partition.
- b. Use Disk Drill to create new partitions.
- c. Specify the size and type for each partition.
- d. Apply the changes to the disk.

# Chapter 12 ♦ Running Yellow Dog Linux 373

# 374 Part III ♦ Choosing and Installing a Linux Distribution

- 9. Configure the firewall. A firewall acts as a conduit between your computer and other computers. If you are connected to networks, enable the firewall. Two choices are available:

- **No firewall** — Don't choose this option, because it does not check requests. Unless your system is not currently providing services, it's best to leave this unchecked.
- **Enable firewall** — The preferred selection. It provides a modulus of security against malicious entities that may want to attack your system. Only the default services are allowed at this level, and you can configure access for more services as needed.
