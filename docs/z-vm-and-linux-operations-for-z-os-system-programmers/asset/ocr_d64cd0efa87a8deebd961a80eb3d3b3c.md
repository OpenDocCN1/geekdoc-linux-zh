To set up minidisk space for LNXMAINT:

+   1. Edit the USER DIRECT file and add the following user ID definition to the bottom of the file:

```
==> x user direct c
====> bottom
====> a 6
...
USER LNXMAINT LNXMAINT 64M 128M BEG
INCLUDE IBMDFLT
LINK TCPMAINT 592 592 RR
MDISK 0191 3390 <2050> 0020 <LX6W02> MR READ WRITE MULTIPLE
MDISK 0192 3390 <2070> 0300 <LX6W02> MR ALL WRITE MULTIPLE
*
...
====> file
```

Note the following points for the numbers in black:

+   1 User ID LNXMAINT has the same password; default size of storage (main memory) designated to this user is 64 MB plus 128 MB of extended storage, with class B, E, and G privileges.

+   2 Include the profile named IBMDFLT (which is defined earlier in the USER DIRECT file).

+   3 Link to the TCPMAINT 592 disk is read-only for access to FTP and other TCP/IP commands.

+   4 Define a 191 minidisk of size 20 cylinders from volume LX6W02.

+   5 Define 192 minidisk of size 300 cylinders (approximately 225MB) from volume LX6W02 with the special read password of ALL, which allows read-access from any user ID without a disk password.

+   6 An empty comment line is for better readability.

+   2. When an MDISK statement is added or modified in the USER DIRECT file, always check for overlapping cylinders and gaps (although gaps only leave empty disk space, z/VM allows you to define multiple minidisks over the same disk space, which is not necessarily beneficial). To check, use the DISKMAP command, as previously stated in "Creating a disk" on page 134:

```
==> diskmap user
The minidisks with the END option specified in this directory will not be included in the following DISKMAP file.

File USER DISKMAP A has been created.
```