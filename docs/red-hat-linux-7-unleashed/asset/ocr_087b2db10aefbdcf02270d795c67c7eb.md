First, always make a couple of emergency boot disks. Use the **`mkbootdisk`** command to create a boot disk with your Linux kernel. Then use the **`dd`** command to create a second disk containing the **`rescue.img`** file from the Red Hat Linux CD-ROM. Use the **`mount`** command to mount the CD-ROM:

```
```
# mount /mnt/cdrom
```
```

Log in as the **root** operator, insert a blank floppy disk in your computer (label it **rescue**), and then create the rescue disk, using **`dd`** to copy the **`rescue.img`** file:

```
```
# dd if=/mnt/cdrom/images/rescue.img of=/dev/fd0 bs=1440k
```
```

Boot Linux from your Red Hat Linux boot disk. Next, at the **boot:** prompt, type **rescue**, which loads a kernel from the disk. Follow the prompts and, when asked, eject the boot disk and insert the second rescue disk. You'll end up with a **# bash** shell prompt.

Under the **`/bin`** directory, you'll find a minimal set of programs to help you recover your files. Remember, the idea is to at least get you where you can try to check your existing partitions and possibly mount your drive. For example, if you have a Linux partition on **`/dev/hda5`**, you can try to first create a mount point by using the **`mkdir`** command, and then use **`mnt`** to mount your partition:

```
```
# mkdir /mnt/linux
# mount -t ext2 /dev/hda5 /mnt/linux
```
```

Your Linux partition will be found under **`/mnt/linux`**, and you can then attempt a fix or copy important files.

If you've installed Red Hat Linux and for some reason your system won't boot—and you don't have your Red Hat boot disks—you can also try booting directly from the first Red Hat Linux CD-ROM. (You might have to change your **BIOS** settings to alter the boot device sequence from your hard drive or floppy drive.)

You can also try to reboot your computer to **DOS**, change the directory to the CD-ROM and then **DOSUTILS**, and then type **AUTOBOOT**, which will execute the **AUTOBOOT.BAT** batch file and put you into the Red Hat installation process.

# ## For More Information

For more information about the **`linuxconf`** tool, navigate to **http://www.solucorp.qc.ca/linuxconf**.

To subscribe to the **`linuxconf`** mailing list, put the following text into the body of an email message addressed to **linuxconf-request@solucorp.qc.ca**:

```
```
subscribe linuxconf
```
```