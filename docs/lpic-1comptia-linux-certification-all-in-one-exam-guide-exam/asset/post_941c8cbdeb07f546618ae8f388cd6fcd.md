
5. A file named myapp has a mode of 755. If nelson doesn't own this file and isn't a member of the group that owns the file, what can she do with it?
- A. She can change the group that owns the file.
- B. She can open the file, make changes, and save the file.
- C. She can change ownership of the file.
- D. She can run the file.

6. You need to change the permissions of a file named schedule.odt so that the file owner can edit the file, users who are members of the group that owns the file can edit it, and users who are not owners and don't belong to the owning group can view it but not modify it. Which command will do this?
- A. chmod 664 schedule.odt
- B. chmod 555 schedule.odt
- C. chmod 777 schedule.odt
- D. chmod 644 schedule.odt

7. Your Linux system's umask variable is currently set to a value of 077. A user named jcarr (who is a member of the users group) creates a file named mythoughts.odt. What can users who are members of the users group do with this file?
- A. They can view the file, but they can't modify or save it.
- B. They can open, modify, and save the file.
- C. They can open, modify, and save the file. They can also execute the file if it is an executable.
- D. They have no access to the file at all.

8. An executable file has the SUID permission set. If this file is run on the system, who owns the file?
- A. The user who created the file remains the owner.
- B. The user who ran the file becomes the file's permanent owner.
- C. The user who ran the file becomes the file's temporary owner.
- D. The root user becomes the file's owner.

9. A directory is owned by the users group and has a mode of rwxrwxr--- permissions assigned to that group. It also has the Sticky Bit permission set. What effect does this have on files within the directory?
- A. Users who are members of the users group can only delete files within the directory for which they are the owner.
- B. No user is allowed to delete files in this directory.
- C. Users who are members of the users group can delete any file within the directory.
- D. Others can enter the directory and delete files within the directory for which they are the owner.

10. Which mount options need to be included in /etc/fstab to enable quotas when a file system is mounted? (Choose two.)
- A. groupquota=on
- B. usrquota
- C. grpquota
- D. userrquota=on
- E. fsquota

11. With the quota package installed on your Linux system, what parameters can you set quotas for in the file system? (Choose two.)
- A. Blocks
- B. Permissions
- C. Inodes
- D. Ownership
- E. Number of Users
- F. Number of Groups

12. Which command is used to create quota files for the file system where quotas have been enabled.
- A. quotacheck -amvug
- B. quotaon -av
- C. repquota -av
- D. edquota -u

## Answers

1. D. Entering chown dnelson:editors /var/opt/runme will change the user and group owners of the runme file to dnelson and editors.
2. C. The execute permission allows a user to enter a directory in the file system.
3. A, B. The user must have read and write permissions to open and modify a file.
4. A. In the mode shown, Group is given the read permission only. Because mnhuffman is a member of the group, he can only open and view file contents. He can’t modify and save the file.
5. D. Because dnelson isn’t the owner and isn’t a member of the owning group, she is granted the rights assigned to Others, which are read (4) and execute (1). This allows her to run the file.
6. A. Entering chmod 664 schedule.odt will grant Owner and Group read (4) and write (2) permissions. It will also grant Others read (4) permission.
7. D. Because umask is set to 077, all permissions (read=4, write=2, execute=1) are removed from Group and Others. Therefore, members of the owning group have no access to the file.
8. C. The SUID permission causes the user who runs the file to temporarily become the file's owner.
9. A. The Sticky Bit permission negates the effect of the group write permissions. As a result, users who are members of the users group can only delete files within the directory for which they are the owner.
10. B, C. You need to add the usrquota and grpquota options to the mount options for the file system.
11. A, C. The quota package can set quotas on blocks and inodes in the file system.
12. A. The quotacheck -amvug command is used to create quota files for the file system where quotas have been enabled.

# MANAGING HARDWARE UNDER LINUX

In this chapter, you will learn about:
- Managing PC hardware
- Working with Linux drivers

This is going to be a fun chapter! As I mentioned earlier in this book, I'm a true techie at heart. I love playing with PC hardware. I spend way too much time scouring hardware vendor catalogs and far too much money ordering new parts. (My local UPS delivery driver and I are on a first-name basis.) Every computer I own is a "Frankenstein" system made of a variety of parts from many different sources.

In this chapter, I'm going to discuss how to manage hardware in your system and configure Linux to support it.

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_472_0.png)

> EXAM TIP For your LPIC-1/CompTIA Linux+ exam, you need to be very comfortable working with PC hardware in a Linux environment. Expect to see several questions about loading kernel modules and installing codecs. Be sure you know where kernel modules are stored in the system and the commands that are used to manage them.

Let's begin this chapter by discussing how to manage PC hardware.

# Managing PC Hardware

For your LPIC-1/CompTIA Linux+ exam, you need to be very familiar with the tasks and procedures associated with managing PC hardware. I'm going to make an assumption at this point that you already have a fairly good understanding of the basics of PC hardware and that I don't need to go into a review of basic PC hardware. For this chapter, I'm going to assume that if I were to open a PC case and show it to you, I could ask you to point out the various components that compose the system, including the following:

- Motherboard
- CPU
- RAM
- Hard drive
- Optical drive
- Expansion slots
- Power supply
- Various motherboard connectors
- And so on...

Accordingly, in this chapter we will focus on the hardware skills and tasks specified in the LPIC-1/CompTIA Linux+ exam objectives. The following topics will be addressed:

- Identifying mass storage devices
- Working with removable hardware interfaces
- Managing system resources
- Managing integrated devices
- Managing systems without external peripherals

Let's begin by learning how to identify the various types of mass storage devices.

## Identifying Mass Storage Devices

As you already know, your *random access memory* (RAM) is the place in a computer system where programs and data currently in use on the system are stored. The key benefit of RAM is the fact that it is very fast. Data in RAM can be accessed very quickly because the CPU can directly access any memory location at any time. This makes it an ideal storage device for data that needs to be manipulated by the CPU.

For example, suppose you need to create a word-processing document. The first thing you need to do is open your word-processing application. When you do, the program code for the application is loaded from your hard disk drive into RAM. When you open a word-processing file in the application, the data you are working on is also loaded into RAM.

While RAM is fast, it does have one key drawback. It has to be constantly refreshed with electricity every few milliseconds. If the system fails to do this, then the data and programs stored in RAM are forever lost. The DRAM we use for system memory is really fast, but it isn't *persistent*. To make a PC system truly usable, we need some kind of long-term, persistent storage medium that will retain data even if the power to the system is shut off.

In this topic, we're going to review several storage devices that can do just that. We'll cover the following:

- Floppy diskettes
- Hard disk drives
- Solid-state drives
