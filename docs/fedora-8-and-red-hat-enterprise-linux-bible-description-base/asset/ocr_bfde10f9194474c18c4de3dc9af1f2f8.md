The first step is to create an image of the CD file system as a file on your computer. You do this with the mkisofs command. The second step is to burn the image to CD or DVD using a tool such as the cdrecord command.

> **NOTE:** In recent releases of Fedora, the cdrecord command has been replaced by a command called wodm from the CDR Kit project (http://cdrrkit.org). Fedora and other Linux distributions switched to the CDR Kit project because cdrecord licensing was changed to the Sun CDDL license, which is believed to be incompatible with the GPL. Because wodm is backward compatible with cdrecord and that command is linked to cdrecord, you can still use the cdrecord command as you always have.

As an example, imagine that you want to back up the home directory for user mary. You would invoke the mkisofs command and pass it the name of the file system image file to create, followed by the directory to base it on:

```
$ mkisofs -R -O /var/tmp/mary.iso /home/mary
```

This creates an ISO9660 file system image in a file named mary.iso located in the /var/tmp directory. The -R option causes Linux-specific file ownership and long filenames to be used. If your /var partition does not have enough room for the image, choose a different location.

> **TIP:** By default, mkisofs preserves the ownership and access rights of files and directories when it creates the file system image. This is appropriate when you are making a backup, but not when you are creating a software distribution CD. In such a case, add the -R option instead of -r as the first parameter to mkisofs. It will then store all files as publicly readable and, where appropriate, executable.

If you have an ATAPI CD drive, you no longer need a SCSI ID for that drive to be able to record to it. You could enter the device name instead of the SCSI ID (such as dev=/dev/cdrom). However, if you have a SCSI CD drive, before you can write the image file to a CD, you must first discover the SCSI bus number, device ID number, and Logical Unit Number (LUN) of the CD drive. You can find out which SCSI device ID the CD drive is using. Invoke the cdrecord command with the single parameter -scanbus:

```
# cdrecord -scanbus
```

You should see a response similar to the following:

scsibus0:
0,0,0 0) 'IDE-CD' 'R/W 4x4x24 1.04' Removable CD-ROM
0,0,1 1)              
0,0,2 2)              
0,0,3 3)              
0,0,4 4)              
0,0,5 5)              
0,0,6 6)              
0,0,7 7)