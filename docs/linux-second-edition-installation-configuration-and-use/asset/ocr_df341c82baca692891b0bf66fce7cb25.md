# FILE SYSTEM ADMINISTRATION 147

authentication of users. Configuration of PAM is carried out via the files in /etc/pam.d. Comprehensive documentation can be found in /usr/doc/pam-n.

# Access privileges

As root, you automatically have access to all system files and devices (devices like files and allow access to the hardware — such as /dev/tty1 for the second reality interface which is often connected to a modem). If instead, log in as a normal user without root privileges, you will find that a number of devices are denied to you: you can no longer access diskette devices, you cannot use the modem, and so on.

On single-user systems this is easily remedied by specifying more liberal settings for the rights to access devices. You simply log as root, change to the /dev directory and execute the following chmod command for the devices in question:

```
# cd /dev
# chmod a+rw fd *
```

/dev/fd* (all devices that point to floppy disk drives) must be substituted by the relevant name, such as ttyS* for the serial interfaces, lp* for the parallel interfaces (printers), and so on.

If you are not the only person to work on your computer, chmod a+rw represents a considerable security risk. You can distribute access privileges in a more controlled manner by listing those users in specific groups (for example, wctp in /etc/group who are allowed to access files or devices of that group (for example, the serial interface for modem use). Thus you can leave the bits of the device files unaltered. You will find further information about access privileges from page 90 onward.

![](bbox=[0.131, 0.445, 0.175, 0.553])

# 6.5 File system administration

If Linux is properly configured, you can access various hard disk partitions, the CD-ROM, and so on, immediately after the system has started up. This section will deal mainly with the fstab file, which is responsible for all this. Furthermore, we describe how to create swap partitions and swap files.

TIP Additional background information about the internals of the file system can be found in Chapter 5 from page 100 onward.

![](bbox=[0.131, 0.725, 0.175, 0.759])

# The fstab file

/etc/fstab file specifies which storage devices are to be mounted into the file system. In any case, fstab must contain the following two lines (which, depending on your configuration, may look slightly different). Further hard disk partitions, CD-ROMs and diskettes can be mounted manually using the mount command.