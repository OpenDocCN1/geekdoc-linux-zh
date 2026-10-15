
### Example 4-12 Boot parameter file for Linux guest LNXCER

```
ramdisk_size=65536 root=/dev/ram0 ro init=/linuxrc TERM=dumb
hostip=<9.12.5.65> hostname=<ceron>
gateway=<9.12.4.1> netmask=<255.255.254.0>
broadcast=<9.12.7.255> layer2=0
readchannel=0.0.0600 writechannel=0.0.0601 datachannel=0.0.0602
nameserver=<9.12.6.7> portname=dontcare
install=<ftp://totibim:itso@9.12.4.69/code/sles10x>
instnetdev=osa osainterface=qdio osamedium=eth Manual=0
usessh=1 sshpassword=letmein
```

Make sure that you replace the \<value\> entries with the values that correspond to your resources according to your planning worksheet at Appendix B, "Planning worksheet" on page 403. Also, do not forget the last line highlighted in bold because in this book we instruct you to perform an SSH installation of SLES10.

## Setting up common profiles for the Linux VMs

To enable all Linux guests to see the 192 disk you created for LNXMAINT with all of the common files for boot, you have two options:

- The labor-intensive method is to put a LINK statement for every user description in MAINT's USER DIRECT file.

- The easier method is to create a profile based on the default profile and add the proper lines for the link statements. Then, to make use of them, all you have to do when creating a Linux guest user is to import this new profile.

Our examples are based on the second approach, of course.

To enable all Linux guests by using the easier method:

- 1. Logon to MAINT and edit the USER DIRECT file:

    ```
    ==> x user direct c
    ```

In the USER DIRECT file, you can group statements that will be common to many user definitions in a construct called a profile. This profile can then become part of user definitions by using the INCLUDE statement. You used the existing profile TCPCMSU when you defined the LNXMAINT user.

- 2. Create a new profile named LNXDFLT. This will contain the user directory statements that are common to all Linux user IDs. To save typing, use the "*" prefix commands to duplicate the IBMDFLT profile that should be on lines 37-50:

    ```
    00037 **************************************************
    00038 *
    00039 PROFILE IBMDFLT
    00040  SPOOL 000C 2540 READER *
    00041  SPOOL 000D 2540 PUNCH A
    00042  SPOOL 000E 1403 A
    00043  CONSOLE 009 3215 T
    00044  LINK MAINT 0190 0190 RR
    00045  LINK MAINT 019D 019D RR
    00046  LINK MAINT 019E 019E RR
    00047  LINK MAINT 0402 0402 RR
    00048  LINK MAINT 0401 0401 RR
    00049  LINK MAINT 0405 0405 RR
    00050 *******************************
    ```

- 3. Edit the duplicated profile by deleting the three LINK MAINT 040x lines, and inserting the lines that are in bold text from Example 4-13. See the notes following example.

### Example 4-13 Profile LNXDFLT

```
PROFILE LNXDFLT
IPL CMS
MACHINE ESA 4
CPU 00 BASE
CPU 01
NICDEF 600 TYPE QDIO LAN SYSTEM VSW1
SPOOL 000C 2540 READER *
SPOOL 000D 2540 PUNCH A
SPOOL 000E 1403 A
CONSOLE 009 3215 T
LINK MAINT 0190 0190 RR
LINK MAINT 019D 019D RR
LINK MAINT 019E 019E RR
LINK LNXMAINT 192 191 RR
LINK TCPMAINT 592 592 RR
```

Notes about the example:

- 1 IPLs CMS when the user ID logs on.
- 2 Identifies machine as type ESA with a maximum of 4 CPUs that can be defined.
- 3 Defines the base CPU.
- 4 Defines a second CPU; do not include this if your LPAR has only a single Real IFL/CP.
- 5 Defines a virtual NIC connected to the VSWITCH starting at virtual address 600.
- 6 Provides read access to the LNXMAINT 192 disk as the user's 191 disk.
- 7 Provides read access to the TCPMAINT 592 disk, so that the user has access to TCPIP services such as an FTP client.

- 4. Save the file:

    ```
    ====> file
    ```

## Create the first Linux VM

In the virtualization discussion in section 2.2.1, "History of z/VM" on page 14, all you have to do to create a virtual machine in which Linux can run is to create a z/VM user. The first thing to do is to set up the user minidisks.

### Setting up minidisks

Create a new user for your Linux guest and set up its minidisks exactly the same way you did for the LNXMAINT user in "Setting up minidisk space for LNXMAINT" on page 183. Log on as MAINT and add a new user definition into the USER DIRECT C file. This is your first user to include the LNXDFLT profile you created in "Setting up common profiles for the Linux VMs" on page 193. Example 4-14 shows a template you can use.

### Example 4-14 Create the Linux guest user.

```
user <lnxcer> <lnxcer> 512M 2G BDEG
include lnxdflt
option lnknopas applmon
mdisk 100 3390 0001 3338 <nwla25> mr lnx4vm lnx4vm lnx4vm
mdisk 103 3390 0001 3338 <nwla26> mr lnx4vm lnx4vm lnx4vm
mdisk 104 3390 0001 3338 <nwla27> mr lnx4vm lnx4vm lnx4vm
mdisk 105 3390 0001 3338 <nwla28> mr lnx4vm lnx4vm lnx4vm
mdisk 106 3390 0001 3338 <nwla29> mr lnx4vm lnx4vm lnx4vm
```

The example defines this Linux user ID as having the following minidisks and virtual disks:

- 100 A minidisk to hold the /boot partition; the remaining space is given to the system LVM, where all other partitions will be located. More about Linux LVM is described in "Linux Logical Volume Manager" on page 307.
- 101-102 These are virtual disk (VDISK) swap spaces created by SWAPGEN EXEC upon logging on. They are not defined in USER DIRECT, but dynamically in the user's PROFILE EXEC when the user ID logs on.
- 103-106 These minidisks are to be managed by the Linux system LVM.
