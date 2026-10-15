If neither of these options is feasible for you, you can use the install floppy disk (see the preceding section on creating a boot disk). This is perhaps the most fail-safe method of installing Linux. Insert the Linux install disk into your floppy drive and reboot your computer.

The installation program will start, presenting you with an introduction screen. After a moment, the following prompt will appear at the bottom of your screen:

```
boot:
```

Press ENTER. (If necessary, you can enter boot parameters as described in the installation manual.) Configuration information will fill your screen as the installation program attempts to detect your hardware components automatically.

Your system then detects your hardware, providing any configuration specifications that may be needed. For example, if you have an IDE CD-Write drive, it will be configured automatically as a SCSI drive so that CD writing software can make use of it (see Chapter 31). If you are installing from a floppy disk, it will detect your CD-ROM. If for some reason it cannot do so, your system will ask you to select your CD-ROM from a list. If you still have difficulty, you may have to specify the CD-ROM at the boot prompt.

```
Boot: linux hdx=c drom
```

Replace the x with one of the following letters, depending on the interface the unit is connected to, and whether it is configured as master or a slave:

+   - a First IDE controller master
+   - b First IDE controller slave
+   - c Second IDE controller master
+   - d Second IDE controller slave

> Note As each screen appears in the installation, default entries will be already selected, usually by the autoprobing capability of the installation program. Selected entries will appear highlighted. If these entries are correct, you can simply click Next to accept them and go on to the next screen.

# Partitions, RAID, and Logical Volumes

You will initially be asked to set up and designate the Linux partitions and hard disk configurations you want to use on your hard drives. Red Hat provides automatic partitioning options if you just want to use an entire single hard drive for your Linux system. To manually configure your hard disks, Red Hat provides a very detailed and graphic-oriented partitioning tool called Disk Druid. With Disk Druid, you can create specific partitions, or configure RAID devices, or set up logical volumes (see Chapter 31).

Once you have configured your hard disks, your partitions will be formatted. If you are formatting any old Linux partitions that still have data on them, a dialog box will appear listing them and asking you to confirm that you want to format them (new Linux partitions that you created will automatically be formatted). If you already have a Linux system, you will most likely have several Linux partitions already. Some of these may be used for just