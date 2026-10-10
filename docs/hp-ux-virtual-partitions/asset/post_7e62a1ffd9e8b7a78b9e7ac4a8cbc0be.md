
After adding all of this information, you have configured the initial administrator account. As we'll see later, you can add subsequent administrator and operator accounts to the Secure Web Console.

The next screen (Figure 3-6) shows the network-related configuration we'll make to the Secure Web Console. Since it came with a pre-configured IP address, we'll now assign the dedicated IP address for the device.

![](img/eff8b9287a5f38c5adf538f24aacf29e_189_0.png)

In Figure 3-6 I show the two types of terminals that you can select. In this "Configure IP" screen, you'll enter both a name for the Secure Web Console and the computer to which it is connected. All of the IP-related information is entered in this screen as well. The Secure Web Console requires a dedicated IP address because you connect directly to it to make a console connection to the HP 9000.

When all of the information has been added, we select "OK" on this screen and are shown the following message in Figure 3-7:

![](img/eff8b9287a5f38c5adf538f24aacf29e_190_0.png)

Figure 3-7 Initial Secure Web Console Setup Complete

After we select "OK" in Figure 3-7, we can reconnect to the Secure Web Console using the IP address we assigned to it during the configuration. In our case, we would use http://15.88.85.14 to reconnect, as shown in Figure 3-8:

![](img/eff8b9287a5f38c5adf538f24aacf29e_191_0.png)

Figure 3-8 Secure Web Console Login Screen

We log in with the name and password we earlier defined for the Secure Web Console administrator and are then connected as shown in Figure 3-9:

![](img/eff8b9287a5f38c5adf538f24aacf29e_192_0.png)

Figure 3-9 Secure Web Console Menu

At this point, you can select from a number of Secure Web Console-related functions to perform, such as configuring additional users, or you can access the console on your HP 9000, which is the purpose of connecting the device. The Access console selection gives us the console of the HP 9000, as shown in Figure 3-10:

![](img/eff8b9287a5f38c5adf538f24aacf29e_193_0.png)

Figure 3-10 Initial Secure Web Console Screen

Notice that we are logged in as root when we select *Access console*. You could use the Secure Web Console menu to configure additional administrators and operators (we configured only one administrator in our example and no operators) to give multiple users access to your HP 9000 through the Secure Web Console.

The Secure Web Console can be a good alternative to using a dedicated console on each HP 9000. I wanted to provide you with the basic information for configuring the Secure Web Console, the URL for the configuration document, and an overview of the product to help you determine if it is right for your environment.

# Configuring the Guardian Service Processor (GSP)

The Guardian Service Processor (GSP) is a built-in processor on most HP 9000 systems, such as the L-Class and N-Class, that can be used for either local or remote system administration functions. I won't cover the use of the GSP, but I will cover its initial configuration. The initial configuration is important because the first person to gain access to the GSP before it has been configured is a GSP administrator by default.

You gain access to the GSP with ^b (control b). If the GSP has not been configured, anyone who gets access to the console can type ^b and gain access to the system. I recommend that you perform GSP configuration as soon as possible after installing your system.

The following example shows issuing a ^b, which results in the GSP> prompt, and issuing he for help:

```text
Service Processor login:
Service Processor password:

          Hewlett-Packard Guardian Service Processor

          9000/800/12000-44 System Name: uninitialized

GSP Host Name:  uninitialized
GSP>
GSP Host Name:  uninitialized
GSP> he


he
HE
AC : Alert Display Configure            PC : Power Control
AR : Config. Automatic System Restart  PS : Power Management Module status
CA : Configure serial port parameters   RP : Reset password configuration
CP : Log repair info in history buffer  RS : System reset through RST signal
CL : Display console history            SUM : Set Display Mode (hex or text)
CC : Return to Console Mode            SS : Activate a system session
C : Default configuration               SL : Display SPU status logs
D1 : Disconnect remote or LAN console   SO : Security options & access control
DR : Disable remote or LAN console      SS : System's processor status
ER : Enable remote or LAN console       TC : System reset through INIT signal
NB : Display the available commands     TS : Sends a message to other terminals
IT : Modify GSP inactivity timeouts     VFF : Activities Alert Log Display
LC : Configure LAN console               WHO : Displays list of GSP connected users
LS : Display LAN console status          XD : GSP Diagnostic and Reset

MR : Modem Reset
MS : Display the status of the Modem

XU : Upgrade the GSP Firmware

GSP Host Name: uninitialized
GSP:
```

You can see that in order to log in after the `^b` was issued, neither a login name nor a password were required. This is because GSP users have not yet been configured, so anyone can get access to this menu with `^b` at the system console.

There are several commands here to which you don't want unauthorized users to have access, so the first step we'll take is to set up security with SO:

```text
GSP> so
SO
This command allow you to modify the security options and access control.
GSP wide parameters are:
. Login Timeout: 1 minutes.
. Number of Password Faults allowed: 3
. Flow Control Timeout: 5 minutes.
Do you want to modify the GSP wide parameters? (Y/N)

User number 1 parameters are:
. User's Name:
. User's Login:
. Organization's Name:
. Dial-back configuration: Disabled
. Access Level: Operator
. Mode: Simple
. User's state: Disabled
Do you want to modify the user number 1 parameters? (Y/N/Q to quit) :
```

From this menu you can change GSP-wide parameters and establish GSP users. The first user added the first time you enter this screen will be the GSP system administrator. This is the user you want to set initially so your system is secure. You can add one administrator and 19 users. This is an important step since users will now have to add a username and password to gain access to GSP. The user information you add is shown in the preceding listing and is self-explanatory.

# Configuring the Guardian Service Processor (GSP)

In addition to configuring users, there are many useful features of GSP, so I encourage you to experiment with it. One feature I often use is to issue **CL** to display a console history as shown in the following listing for the L-Class system used throughout the examples in this chapter:

```text
> cl

1.

Firmware Version 39.46
Duplex Console IO Dependent Code (IODC) revision 1

(C) Copyright 1995-1998, Hewlett-Packard Company, All rights reserved
Processor State CoProcessor State Cache Size
Number Speed Inst Data
0 440 MHz Active, Functional 512 KB 1 MB
1 440 MHz Idle Functional 512 KB 1 MB
Central Bus Speed (in MHz) : 62
Available Memory : 2097152 KB
Good Memory Required : 11468 KB
```

Press Q/q to quit, Enter to continue:

```text
Primary boot path: 0/0/1/1.2
Alternate boot path: 0/0/2/0.2
Console path: 0/0/4/0.0
Keypad path: 0/0/4/0.0

WARNING: The non-destructive test bit was set, so memory was not tested
 destructively. Information only, no action required.

Processor is booting from first available device.
To discontinue, press any key within 10 seconds.
10 seconds expired.
Processing...
Trying Primary Boot Path
.
Booting...
Boot IO Dependent Code (IODC) revision 1
```

Press Q/q to quit, Enter to continue:

```text
HARD Booted.
ICL Revision A.00.38 OCT 26, 1994
ICL booting hpx
Boot
: disk(0/0/1/1.2.0.0.0.0.0.0;/stand/ovmanix
6340608 + 821576 + 695024 start 0x210ce8

alloc_pdc_pages: Relocating PDC from 0xf0000000 to 0xf7ab000.
gste04: svsev_cd00: 0x00002000 for 1 pages
Unexpected interrupt on EBR bit 32
NOTICE: aoutfs_link(): File system was registered at index 3.
NOTICE: nfsl_link(): File system was registered at index 5.

System Console is on the Built-In Serial Interface
Logical volume 64, 0x3 configured as ROOT
Logical volume 64, 0x2 configured as SWAP
Logical volume 64, 0x2 configured as DUMP
Swap device table: (start & size given in 512-byte blocks)
entry 0 = major is 64, minor is 0x2; start = 0, size = 2097152

Starting the STREAMS daemons-phase 1
Checking root file system.
log replay in progress
replay complete - marking super-block as CLEAN
Root check done.
Create SCSI device files
Starting the STREAMS daemons-phase 2
B2352B/9245XB HP-UX 1B.11.00) #1: Wed Nov 5 22:38:19 PST 1997

Memory information:
  physical page size = 4096 bytes, logical page size = 4096 bytes
  Physical: 2097152 Kbytes, lockable: 1575156 Kbytes, available: 1816368 Kbytes

/sbin/loginctl:
/dev/vg00/lvol0: 34 files, 0 icount, 25716 used, 173665 free (81 frags, 21698 blks, ...)

/sbin/iocheckrc:
Checking for LVM volume groups and Activating (if any exist)
Volume group "/dev/vg00" has been successfully changed.
Activated volume group
Volume group "/dev/vg01" has been successfully changed.
Resynchronized volume group /dev/vg00
Resynchronized volume group /dev/vg01
vxs fsck: sanity check: root file system OK (mounted read/write)
Checking nfs file systems
/sbin/fascienn: /dev/vg00/lvol1 (mounted) ok
NFS file systems are OK, not running fask

Checking vxfs file systems
/dev/vg00/lvol0:
vxfs fsck: sanity check: /dev/vg00/lvol8 needs checking
log replay in progress
replay complete - marking super-block as CLEAN
/dev/vg01/lvol9
vxfs fsck: sanity check: /dev/vg00/lvol9 needs checking
log replay in progress
replay complete - marking super-block as CLEAN
/dev/vg00/lvol3:
vxfs fsck: sanity check: root file system OK (mounted read/write)
/dev/vg00/lvol4:
vxfs fsck: sanity check: /dev/vg00/lvol4 needs checking
log replay in progress
replay complete - marking super-block as CLEAN
/dev/vg00/lvol5:
vxfs fsck: sanity check: /dev/vg00/lvol5 needs checking
log replay in progress
replay complete - marking super-block as CLEAN
/dev/vg00/lvol6:
vxfs fsck: sanity check: /dev/vg00/lvol6 needs checking
log replay in progress
replay complete - marking super-block as CLEAN
/dev/vg00/lvol7:
vxfs fsck: sanity check: /dev/vg00/lvol7 needs checking
log replay in progress
replay complete - marking super-block as CLEAN

(c) Copyright 1983-1997 Hewlett-Packard Co., All Rights Reserved.
(c) Copyright 1979, 1980, 1981, 1985-1993 The Regents of the Univ. of California
(c) Copyright 1980, 1984, 1986 Novell, Inc.
```
