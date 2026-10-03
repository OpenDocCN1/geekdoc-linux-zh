
## INSTRUCTIONAL FEATURES WITHIN THE CHAPTER

These books include a large amount and different kinds of information. The many different elements are designed to help you identify information by its purpose and importance to the exam and also to provide you with varied ways to learn the material. You will be able to determine how much attention to devote to certain elements, depending on what your goals are. By becoming familiar with the different presentations of information, you will know what information will be important to you as a test-taker and which information will be important to you as a practitioner.

> Use the probe-scsi command to obtain a free open SCSI target ID number before adding a tape unit, CD-ROM drive, disk drive, or any other SCSI peripheral. Only devices that are powered on will be located, so make sure that everything is turned on. Use this command after installing a SCSI device to ensure that it has been connected properly and that the system can see it. Also, use this command if you suspect a faulty cable or connection. If you have more than one SCSI bus, use the probe-scsi-all command.

Tip: Tips appear in the margins to provide specific exam-related advice. Such tips may address what material is covered (or not covered) on the exam, how it is covered, mnemonic devices, or particular quirks of that exam.

Note: Notes contain various kinds of useful information, such as tips on the technology or administrative practices, historical background on terms and technologies, or side commentary on industry issues.

Caution: In using sophisticated information technology, there is always potential for mistakes or even catastrophes that can occur through improper application of the technology. Cautions appear in the margins to alert you to such potential problems.

![](img/df66a0e1cd473c73297ad9cbd0cb8_33_0.png)

## STEP BY STEP

### 1.4 Breaking Out of a Hung System

- 1. Use the abort key sequence for your system (Stop+A or L1+A).

The monitor displays the ok PROM prompt.

- 2. Type the sync command to synchronize the disks:

`ok sync`

- 3. When you see the syncing file systems message, press the abort key sequence for your system again.

- 4. Type the appropriate reset command to reset the hardware and start the boot process:

`ok reset`

- 5. After you receive the login: message, log in and type the following to verify that the system is booted to the specified run level:

`# who -r`

- 6. The system responds with the following:

`run-level 3 Jun 9 09:19 3 0 S`

Step by Step: Step by Steps are hands-on tutorial instructions that walk you through a particular task or function relevant to the exam objectives.

Figures: Detailed figures help clarify your understanding of the text.

![](img/df66a0e1cd473c73297ad9cbd0cb8_34_0.png)

FIGURE 19.22
Computers/Networks window

As shown in the pop-up menu on Figure 19.22, you can add a computer to the network.

Double-click the Computers icon, and all of the computers in your domain are displayed, as shown in Figure 19.23.

![](img/df66a0e1cd473c73297ad9cbd0cb8_34_1.png)

FIGURE 19.23
Computers in your domain.

Double-click the specific computer's icon, and the Computers Properties window appears, as shown in Figure 19.24.

![](img/df66a0e1cd473c73297ad9cbd0cb8_34_2.png)

FIGURE 19.24
Computers Properties window.

## EXTENSIVE REVIEW AND SELF-TEST OPTIONS

At the end of each chapter, along with some summary elements, you will find a section called “Apply Your Knowledge” that gives you several different methods with which to test your understanding of the material and review what you have learned.

## CHAPTER SUMMARY

**KEY TERMS**
- OpenBoot
- Bootblock
- ufsboot
- OBP
- NVRAM
- PROM
- POST
- Device Tree
- Full Device Name
- Device Alias

This chapter provided a complete description of the OpenBoot environment; the PROM, the NVRAM, and the kernel.

In this chapter, I described how to access OpenBoot and the various commands available to test and provide information about the hardware.

I described the OpenBoot architecture. I explained how OpenBoot controls many of the hardware devices. Using the programmable user interface available in OpenBoot, the system administrator can set several parameters that control system hardware and peripherals.

Device names were also explained in this chapter. Throughout this book, I will be referring to various device names used in Solaris. It's important that you understand each one of them. I'll revisit this topic in Chapter 16, where devices and device drivers are covered in depth. Along with device names, I explained how to set temporary and permanent device aliases.

**Key Terms:** A list of key terms appears at the end of each chapter. These are terms that you should be sure to know and are comfortable defining and understanding when you go in to take the exam.

**Chapter Summary:** Before the “Apply Your Knowledge” section, you will find a chapter summary that wraps up the chapter and reviews what you should have learned.

**Exercises:** These activities provide an opportunity for you to master specific hands-on tasks. Our goal is to increase your proficiency with the product or technology. You must be able to conduct these tasks in order to pass the exam.

**Review Questions:** These short-answer questions allow you to quickly assess your comprehension of what you just read in the chapter.

## APPLY YOUR KNOWLEDGE

### Exercises

### 4.1 Software Package Administration

This exercise takes you through the task of installing, verifying, and removing software on a Solaris system using the command line.

Estimated Time: 20 minutes

- 1. List the software packages that are currently installed on your system by typing the following:
  `pkginfo`
- 2. Display a long-format listing of information for the SUNWman package installed on your system.
  `pkginfo -l SUNWman`
  What is listed for the status, install date, number of files, and number of blocks used by this package?
- 3. Remove the SUNWdoc package from your system with the following:
  `pkgrm SUNWdoc`
- 4. Use the following commands to verify the presence of SUNWdoc in the default spool area:
- 5. Observe the messages displayed, and verify that the package is installed in /var/spool/pkg.
- 6. Reinstall the SUNWdoc package from the spool area as follows:
  `pkgadd`
- 7. Select the SUNWdoc package when you are prompted, and the package will be reinstalled.
- 8. To remove the SUNWdoc package from the spool area, type the following:
  `pkgrm -s /var/spool/pkg`
- 9. You can now use the pkgchk command to check the completeness, pathname, file contents, and file attributes of the SUNWdoc package:
  `pkgchk SUNWdoc`

### Review Questions

- 1. Which of the following commands is used to show software package information?
  A. pkgadd
  B. pkgchk
  C. pkgparam
  D. pkginfo
- 2. Which of the following commands verifies the accuracy of a software package installation?
  A. pkgadd
  B. pkgchk

## APPLY YOUR KNOWLEDGE

### Answers to Review Questions

1. D. On a standard Solaris file system, a file system cannot span multiple disks or slices. It's only possible when using virtual file systems (that is, DiskSuite).

2. A. Disk configuration information is stored on the disk label.

3. A. The boot block stores the procedures used in booting the system. Without a boot block, the system does not boot.

4. A. The slice information for a particular disk can be viewed by using the prtvtoc command.

5. A. The following are virtual file systems: swapfs, procfs, lofs, cachefs, tmpfs, /var/run, and mntrfs.

6. D. The format utility is used to retrieve corrupted disk labels, repair defective sectors, format and analyze disks, partition disks, and label disks.

7. D. Here are a few of the more important things contained in a superblock:
- Size and status of the file system
- Label (file system name and volume name)
- Size of the file system's logical block
- Date and time of the last update
- Cylinder group size
- Number of data blocks in a cylinder group
- Summary data block
- File system state (clean, stable, or active)
- Pathname of the last mount point

8. A., C. An inode contains all of the information about a file except its name, which is kept in a directory. The inode information is kept in the cylinder information block and contains the following:
- The type of the file (regular, directory, block special, character special, link, and so on)
- The mode of the file (the set of read/write/execute permissions)
- The number of hard links to the file
- The user-id of the file's owner
- The group-id to which the file belongs
- The number of bytes in the file
- An array of 15 disk-block addresses
- The date and time the file was last accessed
- The date and time the file was last modified
- The date and time the file was created

9. B. newfs is the recommended command to create file systems.

10. D. As a general rule, a larger logical block size increases efficiency for file systems in which most of the files are large. Use a smaller logical block size for file systems in which most of the files are small.

11. A. The default number of bytes per inode is 2048 (2KB), which assumes that the average size of each file is 2KB or greater.

12. A. The file system fragment size is the smallest allocatable unit of disk space, which is 1,024 bytes.

Answers and Explanations: For each Review and Exam question, you will find thorough explanations located at the end of the section.
