
## APPLY YOUR KNOWLEDGE
### Exercises
### 15.1 Installing Solaris 8 Using the Interactive Installation Program

For this exercise, you’ll use the interactive installation program to install the Solaris 8 operating environment onto your system.

**Estimated Time:** 1–2 hours depending on the speed of your system and CD-ROM

**Caution:** This exercise will destroy all data on your hard drive.

- 1. Insert the Solaris 8 Installation CD into the CD-ROM drive.
- 2. If the system is currently running, either log in as root and shut the system down, or abort the operating system by pressing Stop+A.
- 3. Boot the operating system from the CD as follows:
- 4. The interactive installation program will begin. Refer to the section titled “Installing Software Using the Interactive Installation Program” and follow the steps outlined in that section for installing the operating system.

```
boot cdrom <return>
```

## Review Questions
- 1. Which of the following is a system that provides services to other systems in its networked environment?
  A. Server
  B. Client
  C. File Server
  D. AutoClientServer

- 2. Which of the following is a system that uses remote services from a server, has limited disk space, and requires a server to function?
  A. AutoClientServer
  B. File Server
  C. Client
  D. Stand-alone

- 3. Which type of installation preserves data?
  A. Initial
  B. Upgrade
  C. Preserve
  D. Web Start

- 4. What are the three phases of the installation process?
  A. System configuration, installation, and post installation
  B. Power on, boot from CD, execute the installation program
  C. Boot from CD, start installation program, post installation
  D. Boot from CD, system configuration, software installation

- 5. Which of the following is not a Software configuration cluster?
  A. Developer System Support
  B. End User System Support
  C. Basic System Support
  D. Entire Distribution Plus OEM System Support

## APPLY YOUR KNOWLEDGE
- 6. Which of the following is Sun’s Java-based installation program?
  A. WebNFS
  B. JumpStart
  C. Interactive Installation
  D. Web Start

- 7. In the interactive software installation program, which of the following file systems are automatically set up for you?
  A. /, swap, /usr, /opt, /var
  B. /, swap, /export/home
  C. /, swap, /usr, /export/home
  D. /, swap, /usr, /opt, /var, /export/home

- 8. Which type of client is known as a “zero administration” client?
  A. The dataless client
  B. The JavaStation
  C. The diskless client
  D. The auto client

- 9. During installation, what is the default software cluster configuration?
  A. End user distribution
  B. Core distribution
  C. Developer distribution
  D. Entire distribution

- 10. What is the kernel architecture of an ultra 1?
  A. sun4m
  B. sun4c
  C. sun4u
  D. sun4

- 11. Which information is not required to install a server system?
  A. The server’s Ethernet address
  B. The server’s hostname
  C. The server’s IP address
  D. The server’s geographic region

## Answers to Review Questions
1. A. A server is a system that provides services or file systems, such as home directories or mail files, to other systems on the network.

2. C. A client is a system that uses remote services from a server. Some clients have limited disk storage capacity, or perhaps none at all; these clients must rely on remote file systems from a server to function.

3. B. The Upgrade option updates the Solaris software to the new release, preserving data and saving as many modifications to the previous version of Solaris software as possible.

4. A. The three phases of the installation process are system configuration, installation, and post installation.

5. C. Solaris 8 software configuration clusters include Entire Distribution plus OEM support (SPARC platform only), Entire Distribution, Developer System Support, User System Support, and Core System Support.

## Apply Your Knowledge
- 6. **D.** Web Start is Sun's Java-based installation program.
- 7. **B.** In the interactive software installation program, /, swap, and /export/home file systems are set up by default.
- 8. **B.** The JavaStation is also known as a zero-administration client. This client has no local file system and its /home is accessed from a server across the network.

- 9. **A.** During the interactive installation, the End User System Support cluster is selected by default.
- 10. **C.** sun4u is the kernel architecture for all Sun Ultra systems.
- 11. **A.** The server's Ethernet address is not required to install a server system. During the installation, you will be prompted to enter the IP address, the hostname, and the geographic region.

## OBJECTIVES
The following test objectives are covered in this chapter:
### Understand device and driver naming conventions
The Solaris operating system accesses devices, such as disks and tape drives, through device path names. The system administrator must be familiar with the various path names that point to each piece of hardware connected to the system.
### Display device and driver configuration information
Solaris provides several methods for displaying information about device drivers. These commands and techniques will be described to help you identify which devices point to which peripherals, and which drivers are loaded in the kernel.
### Configure new devices
The system administrator is responsible for adding and configuring new hardware on the system. This chapter describes how new devices are configured into the Solaris operating environment.

## CHAPTER 16
## Device Administration and Disk Management

## OUTLINE
## STUDY STRATEGIES

| Item | Page |
|---|---|
| Introduction | 567 |
| Device Drivers | 567 |
| Physical Device Name | 568 |
| Device Auto-Configuration | 573 |
| Instance Name | 575 |
| Major and Minor Device Numbers | 578 |
| Logical Device Name | 580 |
| Block and Raw Devices | 581 |
| Virtual Volume Management | 582 |
| Solstice DiskSuite | 583 |
| StorEdge Volume Manager | 586 |
| Chapter Summary | 588 |
| Apply Your Knowledge | 589 |

The following strategies will help you prepare for the test:

- Along with the chapter 13, “The Solaris Network Environment,” this chapter introduces many new terms that you must know well enough to match to a description if it were to appear on the exam. Know the terms I've provided in the “Key Terms” section at the end of this chapter.
- Understand what a device driver is and the various device driver names. They are rather difficult to remember, but keep going over them until you can describe them from memory. Many questions on the exam refer to the various types of device names.
- Practice all the commands and step-by-steps until you can describe and perform them from memory. The best way to memorize them is to practice them repeatedly on a Solaris system.
- Finally, understand the concept of virtual volumes. You don’t necessarily need to know how to create and configure them, but you need to know what they are, and their characteristics. Be prepared to list the advantages of a virtual volume and identify the characteristics and functions of Solstice DiskSuite and the StorEdge Volume Manager.

## INTRODUCTION
Device management in the Solaris 8 environment includes adding and removing peripheral devices, such as tape drives, disk drives, printers, and modems from a system. It might also involve adding a third-party device driver to support a device. System administrators need to know how to specify device names if using commands to manage disks, file systems, and other devices.

This chapter describes disk device management in detail. It also describes disk device naming conventions as well as adding, configuring and displaying information about disk devices that are attached to your system.

## DEVICE DRIVERS
A Sun computer typically uses a wide range of peripheral and mass-storage devices, such as a SCSI disk drive, a keyboard and a mouse, and some kind of magnetic backup medium. Other commonly used devices include CD-ROM drives, printers, and plotters. Solaris communicates with peripheral devices through files called device files or drivers. A device driver is a low-level program that allows the kernel to communicate with a specific piece of hardware. The driver serves as the operating system’s “interpreter” for that piece of hardware. Before Solaris can communicate with a device, the device must have a device driver.

When a system is started for the first time, the kernel creates a device hierarchy to represent all the devices connected to the system. This is the auto-configuration process, which is described later in this chapter. If a driver is not loaded for a particular peripheral, that device is not functional. In Solaris, each disk device is described in three ways, using three distinct naming conventions:

- Physical device name. Represents the full device pathname in the device information hierarchy.
- Instance name. Represents the kernel’s abbreviation name for every possible device on the system.
- Logical device name. Used by system administrators with most file system commands to refer to devices.
