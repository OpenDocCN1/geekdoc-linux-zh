# Chapter 18 ➡ Setting Up Windows Interoperability with Samba 519

![](bbox=[0.137, 0.126, 0.225, 0.175])

If you have problems configuring or using the Winbind daemon, you can use winbind command to query the PDC through the winbind daemon. The information that it returns can help you diagnose Winbind problems by seeing how winbind daemon translates various Windows authentication information. For complete information about the winbind command, type man winbind from the command line within any console, xterm, or other terminal window on your SUSE system.

# Command-Line Utilities for Samba

The Samba software includes a number of utilities that you may find useful when interacting with Windows networks from the Linux command line. The next few sections provide a brief introduction to some of the most useful ones. You can obtain a complete list of all of utilities that are related to Samba by using the apropos command to identify any commands related to Samba or the SMB protocol, in the following examples:

```
whlinux:-> apropos samba
net (8) - Tool for administration of Samba and remote CIFS servers.
smb.conf (5) - The configuration file for the Samba suite
cupsadd (8) - export printers to samba for windows clients
lists (5) - The Samba NetBIOS hosts

whlinux:-> apropos samba
smbpool (8) - send a print to an SMB printer
fs (5) - Linux filesystem types: minix, ext2, ext3, xia, msdos, vfat, proc, iso9660, hfs, sysv, mcfs
sget (1) - wget-like utility for download files over SMB
smbclient (8) - helper utility for mounting filesystems
smb.conf (5) - The configuration file for the Samba suite
cupsadd (8) - export printers to samba for windows clients
testpass (1) - check an anbd configuration file for internal correctness
findbm (1) - list info about machines that respond to SMB name queries on a subnet
smbquotas (1) - Set or get QUOTAS of NTFS 5 shares
smbount (8) - smbfs umount for normal users
smbah (1) - Allows access to remote SMB using UNIX commands
smbount (8) - mount an smbfs filesystem
smbtar (1) - shell script for backing up SMB/CIFS commands directly to UNIX tape drives
smbcls (1) - Set or get ACLs on an NT file or directory names
smbclient (1) - ftp-like client to access SMB/CIFS resources on servers
sbtree (1) - A text based samba network browser
```

The Samba and SMB-related commands that are available on your system will depend on the Samba packages you installed on your system, as explained in the section "Samba Client and Server Packages", later in this chapter.