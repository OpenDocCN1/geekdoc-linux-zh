Just one last thing—you probably don't want to enter the modprobe command every time you reboot your system. It's a good idea to include it as part of your system boot up, for example, in the file /etc/rc.d/boot.local. Just open this file using your favorite editor and add the command modprobe ide-scsi to it. Then, save and exit.

This setup does have one glitch, though, which occurs when you have more than two CD-ROMs. You can have a CD-R/RW and a normal CD-ROM, with both being ATAPI EIDE. This causes both of them to be SCSI emulated. You can control this behavior by having only the CD-R/RW be SCSI emulated while the other CD-ROM remains an ATAPI EIDE device. To do this, you must perform two steps.

The first step is editing /etc/rc.d/boot.local again and adding the command modprobe ide-cd before the modprobe ide-scsi command. It should look like this:

```
modprobe ide-cd
modprobe ide-scsi
```

The second step is modifying the file /etc/modules.conf (in SuSE 6.3) or /etc/conf.modules (SuSE 6.2 and below). Open this file using your favorite editor and add this line to it:

```
options ide-cd ignore=hdd
```

You should replace hdd in the previous line with the device name of your CD-R/RW. Then, save and exit. This tells the ATAPI EIDE CD-ROM module to ignore your CD-R/RW when it loads. The modules will configure all the other CD-ROMs on your system except this one. That finalizes your CD-R/RW setup.

# Crash Course in CD-Writing Tools

Now that you have configured your CD-R/RW to work with Linux, you probably want to know how to write your CDs. You must first install the required tools.

# Package requirements:

# Series ap:

+   - cdrecord
+   - mkisofs

CD-Writing in Linux is not really that hard. It is a two-step process in which you must create what is called an ISO image and then write it on your CD. An ISO image is a file that contains all the files (correctly formatted) you want to write on the CD.

The first step, in which you create the ISO file, is pretty simple. Collect all the files you want to copy to a CD in the same directory. Next, create any subdirectories you want to use and move the files to those subdirectories until you have the final setting you want. Then, run the mkisofs command:

```
# mkisofs -r -o /tmp/cdimage.iso /myfiles
```