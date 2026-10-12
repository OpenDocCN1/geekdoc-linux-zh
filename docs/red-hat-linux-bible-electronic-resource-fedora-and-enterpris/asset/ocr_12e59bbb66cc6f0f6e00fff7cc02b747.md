The first step is to create an image of the CD file system as a file on your computer. You do this with the `mkisofs` command. As an example, imagine that you want to back up the home directory for user mary. You would invoke the `mkisofs` command and pass it the name of the file system image file to create, followed by the directory to base it on:

```
```
$ mkisofs -R -O /var/tmp/mary.cd /home/mary
```
```

This creates an ISO9660 file system image in a file named mary.cd located in the /var/tmp directory. The -R option causes Linux-specific file ownership and long file names to be used. If your /var partition does not have enough room for the image, choose a different location.

> **TIP:** By default, `mkisofs` preserves the ownership and access rights of files and directories when it creates the file system image. This is appropriate when you are making a backup, but not when you are creating a software distribution CD. In such a case, add the -r option instead of -R as the first parameter to `mkisofs`. It will then store all files as publicly readable and, where appropriate, executable.

Before you can write this image file to a CD, you must first discover the SCSI bus number, device ID number, and Logical Unit Number (LUN) of the CD drive. Unless you have an actual SCSI bus in your computer, the emulated SCSI bus is probably numbered zero. You can find out which SCSI device ID the CD drive is using. Invoke the `cdrecord` command with the single parameter `-scanbus`:

```
```
# cdrecord -scanbus
```
```

You should see a response similar to the following:

```
```
Cdrecord 2.0 (i686-pc-linux-gnu) Copyright (C) 1995-2002 Jörg Schilling
Linux sg driver version: 3.1.25
Using libcsc version 'schily-0.7'
scsibus0:
	0,0,0   0) 'IDE-CD ' 'R/RW 4x4x24 '  '1.04' Removable CD-ROM
	0,0,1   1) *  
	0,0,2   2) *  
	0,0,3   3) *  
	0,0,4   4) *  
	0,0,5   5) *  
	0,0,6   6) *  
	0,0,7   7) *  
```
```

This tells you that the CD drive is using SCSI ID zero. The Logical Unit Number in this case should always be zero, so you now have all three numbers. You supply them to `cdrecord` as part of the `dev` parameter. The SCSI bus number is listed first; it is followed by the ID number, and then by the LUN. The entire command should look similar to this:

```
```
# cdrecord -v speed=2 dev=0,0,0 -data /var/tmp/mary.cd
```
```