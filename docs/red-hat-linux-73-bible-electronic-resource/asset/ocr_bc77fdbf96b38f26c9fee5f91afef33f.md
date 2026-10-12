This creates an ISO9660 file system image in a file named mary.cd located in the /var/tmp directory. If your /var partition does not have enough room for the image, choose a different location.

> TIP: By default, mkisofs preserves the ownership and access rights of files and directories when it creates the file system image. This is appropriate when you are making a backup, but not when you are creating a software distribution CD. In such a case, add the -r option as the first parameter to mkisofs. It will then store all files as publicly readable.

Before we can write this image file to a CD, we must first discover the SCSI bus number, device ID number, and Logical Unit Number (LUN) of the CD drive. Unless you have an actual SCSI bus in your computer, the emulated SCSI bus is probably numbered zero. You can confirm this using the dmesg command combined with grep:

```
# dmesg | grep 'scsi'
```

This scans recent kernel messages and prints out any that begin with scsi. For example, if you have an IDE/ATAPI CD drive emulating a SCSI device, you should see output similar to this:

```
scsi0 : SCSI host adapter emulation for IDE ATAPI devices
scsi : 1 host.
scsi : detected 1 SCSI cdrom total.
```

Sure enough, the emulated SCSI bus is identified as scsi0. Next, you need to find out which SCSI device ID the CD drive is using. Invoke the cdrecord command with the single parameter -scanbus:

```
# cdrecord -scanbus
```

You should see a response similar to the following:

```
Cdrecord 1.10 (i686-pc-linux-gnu) Copyright (C) 1995-2001 Jörg Schilling
Linux sg driver version: 3.1.22
Using libscg version 'schily-0.5'
scibus0:
	0,0,0	0) 'Memorex ' 'CRW-1622 ' 'D4.0' Removable CD-ROM
	0,0,1	1) *
	0,0,2	2) *
	0,0,3	3) *
	0,0,4	4) *
	0,0,5	5) *
	0,0,6	6) *
	0,0,7	7) *
```

This tells us that the CD drive is using SCSI ID zero. The Logical Unit Number in this case should always be zero, so we now have all three numbers. We supply them to cdrecord as part of the dev parameter. The SCSI bus number is listed first; it is followed by the ID number, and then by the LUN. The entire command should look similar to this: