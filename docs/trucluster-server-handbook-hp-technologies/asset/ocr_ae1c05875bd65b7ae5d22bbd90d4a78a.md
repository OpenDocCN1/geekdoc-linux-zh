expect to install from HP, third party vendors, or Open Source.

Partitioning the initial Tru64 UNIX system disk can be performed either before you start the Tru64 UNIX installation or during the Tru64 UNIX installation. We will show you two ways in which this can be done, and will leave it to you to determine which way is easier and more efficient.

# 4.2.1.2.1 Partitioning Using the disklabel(8) Command

Partitioning the Tru64 UNIX system disk using the disklabel(8) command is performed before you actually start the installation of Tru64 UNIX. We know, you are asking yourself “How can you use a UNIX command like disklabel and not have Tru64 UNIX installed yet?” Let’s look and see how we do this:

+   - At the first prompt for the Installation of Tru64 UNIX, you would exit the Installation program to edit and write a new disk label on the disk that you will use for Tru64 UNIX.

```
Welcome to the Tru64 UNIX Installation Procedure
This procedure installs Tru64 UNIX onto your system. You will be asked a series of system configuration questions. Until you answer all questions, your system is not changed in any way.

0 The "Exit Installation" option stops the installation and puts your system in single-user mode with superuser privileges. This option is intended for experienced UNIX system administrators who want to perform file system or disk maintenance tasks before the installation. This option may also be used for disaster recovery on a previously installed system.

Remember, you can always get extra information by typing help.
1) U.S. English Installation
2) Installation with Worldwide Language Support
3) Exit Installation
Enter your choice: 3
```

+   - At the shell prompt, set the appropriate terminal type and editor that you will be using to edit the disk label. In our example, we have found that the vt100 terminal type with the vi(1) editor work well.

```
# TERM=vt100; export TERM
# EDITOR=/bin/vi; export EDITOR
```

+   - The next step is to determine which disk to use. You should already have a good idea which disk to use. The issue is finding the right one. In this case, we will use dsk0 as it is the hard disk that is local to the server.

```
# /sbin/bwxmgr -view device
...
67: /dev/disk/cdrom0c        COMPAQ   CD-224E        bus-1-targ-0-lun-0
68: /dev/disk/dak0c          COMPAQ   BD018635C4     bus-5-targ-0-lun-0
...
```