
For the rest of this section I shall assume that you have a 320 MB IDE hard disk, partitioned as in the example in Figure 7.1, with the DOS partition already created and populated with your DOS software. I shall further assume that you wish to install the A, AP, D, K, N, F, X, XAP and Y software sets from the Slackware distribution and that your installation medium will be floppy disks (though the installation procedure is essentially the same from any other installation medium: CD-ROM, hard disk or network).

Once you have the boot and root disks prepared you should insert the boot disk and reboot the machine. Most distributions, Slackware included, provide a boot disk which will allow you to enter hardware configuration details after a prompt. This should only be necessary in the unlikely event that the boot disk kernel fails to detect, correctly identify or configure a particular hardware device.

Our example configuration should present no problems and so you would just press Enter or Return at the prompt to continue with the boot sequence. After a short time you will be prompted to remove the boot disk, replace it with the root disk and press Enter or Return to complete the initial boot sequence.

At this stage, you will have a minimal Linux system, running entirely in memory, using a ramdisk for its root filesystem and, if all has gone well, you should be looking at a Login: prompt. Now, login as root. There is no password set on the account, so you should be able to log straight in.

By convention (one which I shall follow in the examples in this book) the system administrator or super-user is given a prompt which consists of, or at least ends in, a hash (#) symbol. It is a good idea, when used in a prompt, to keep the hash symbol exclusively for this purpose – it will help to avoid confusion.

In order to set up the Linux partitions you need to run fdisk from the hash prompt, which gives an output as follows:

```
# fdisk
Using /dev/hda as default device!

Command (m for help):
```

The file name /dev/hda is the device special file name corresponding to the whole of the first hard disk drive (/dev/sda for a SCSI disk). This is the drive that fdisk tries to work with by default. If you have a second hard drive, you can get fdisk to work with that instead by specifying the pathname to the device special file for the second drive (/dev/hdb or /dev/sdb) as a parameter to the command:

```
# fdisk /dev/hdb
```

Under Linux, every disk drive and partition is given a name in /dev. These names appear as follows:

- hda entire hard drive 1;
- sda entire SCSI hard drive 1;
- hdb entire hard drive 2;
- sdb entire SCSI hard drive 2;
- fd0 entire floppy drive 0 (DOS A:);
- fd1 entire floppy drive 1 (DOS B:).

The partitions on any of the hard drives can be accessed just by adding the appropriate number to the name for the entire drive. The following table shows how to name the partitions on drive hda:

- hda1 hard drive 1, primary partition 1;
- hda2 hard drive 1, primary partition 2;
- hda3 hard drive 1, primary partition 3;
- hda4 hard drive 1, primary partition 4;
- hda5 hard drive 1, logical partition 1;
- hda6 hard drive 1, logical partition 2;
- hda7 hard drive 1, logical partition 3, etc.

The Linux fdisk command looks different to the DOS equivalent, but they both perform similar functions. You can obtain a list of the functions by using the ‘m’ command once you have fdisk running:

```
# fdisk
Using /dev/hda as default device!

Command (m for help): m
Command action
  a  toggle a bootable flag
  c  toggle the dos compatibility flag
  d  delete a partition
  l  list known partition types
  m  print this menu
  n  add a new partition
  p  print the partition table
  q  quit without saving changes
  t  change a partition's system id
  u  change display/entry units
  v  verify the partition table
  w  write table to disk and exit
  x  extra functionality (experts only)
```

A sensible thing to do at this point is to display the existing partition table, with the ‘p’ command, to check that the DOS partition has been set up properly:

```
Command (m for help): p

Disk /dev/hda: 16 heads, 40 sectors, 1024 cylinders
Units = cylinders of 640 * 512 bytes

    Device Boot Begin Start  End Blocks Id System
    /dev/hda1   *       1     1   511 163812+  6  DOS 16-bit >=32M
```

It has, so now you can set up the Linux partitions, starting with the swap space on /dev/hda2. You use the ‘n’ command to add a new partition, and then fdisk will ask you if you want to create a primary or extended partition. In our example, we want a primary partition, so you would answer ‘p’ to this prompt. You will then be asked which partition number to use and you would answer ‘2’. The next question from fdisk asks you to specify at which disk cylinder the new partition should start. In answer to this question, you should give the number of the next free cylinder, after the DOS partition. This will be 512 here. The last question asks you to specify where the new partition ends. This can be given as a cylinder number or you can just specify how big you want the partition in either bytes, kilo-bytes or mega-bytes. To specify a 16 Mb swap partition you would answer ‘+16M’. The whole sequence appears as:

```
Command (m for help): n
Command action
  e   extended
  p   primary partition (1-4)

p
Partition number (1-4): 2
First cylinder (512-1023): 512
Last cylinder or +size or +sizeM or +sizeK (512-1023): +16M
```

Incidentally, there is nothing to stop you from having multiple swap partitions. If for instance you have more than one hard disk then this arrangement might be the most convenient.

After creating the partition to be used for swap space, a similar sequence can be followed for the Linux root partition on /dev/hda3:

```
Command (m for help): n
Command action
  e   extended
  p   primary partition (1-4)

p
Partition number (1-4): 3
First cylinder (564-1023): 564
Last cylinder or +size or +sizeM or +sizeK (512-1023): 1023
```

A ‘p’ command at the end of this sequence will confirm that all has gone according to plan:

```
Command (m for help): p

Disk /dev/hda: 16 heads, 40 sectors, 1024 cylinders
Units = cylinders of 640 * 512 bytes
```

| Device | Boot | Begin | Start | End | Blocks | Id | System |
|---|---|---|---|---|---|---|---|
| /dev/hda1 | * | 1 | 1 | 511 | 163812+ | 6 | DOS 16-bit >=32M |
| /dev/hda2 |  | 512 | 512 | 563 | 16640 | 83 | Linux native |
| /dev/hda3 |  | 564 | 564 | 1023 | 147200 | 83 | Linux native |

This is looking good. However, there is just one more thing to do to finish it off. The system type for partition 2 is still flagged as Linux native when it should be Linux swap. This can be corrected with the ‘t’ command to toggle the Id from 83 to 82. How do I know what the number should be? You can get fdisk to give you a list when you use the ‘t’ command:

```
Command (m for help): t
Partition number (1-4): 2
Hex code (type L to list codes): L
```

|  |  |  |  |
|---|---|---|---|
| 0 Empty | 8 AIX | 75 PC/IX | b7 BSDI fs |
| 1 DOS 12-bit FAT | 9 AIX bootable | 80 Old MINIX | b8 BSDI swap |
| 2 XENIX root | a OS/2 Boot Man | 81 Linux/MINIX | c7 Syrinx |
| 3 XENIX usr | 40 Venix 80286 | 82 Linux swap | db CP/M |
| 4 DOS 16-bit <32M | 51 Novell? | 83 Linux native | e1 DOS access |
| 5 Extended | 52 Microport | 93 Amoeba | e3 DOS R/O |
| 6 DOS 16-bit >=32M | 63 GNU HURD | 94 Amoeba BBT | f2 DOS sec |
| 7 OS/2 HPFS | 64 Novell | a5 BSD/386 | ff BBT |
| Hex code (type L to list codes): 82 |  |  |  |

And now, at last, the partition table should be set up as required. A final look just to make sure:

```
Command (m for help): p

Disk /dev/hda: 16 heads, 40 sectors, 1024 cylinders
Units = cylinders of 640 * 512 bytes
```

| Device | Boot | Begin | Start | End | Blocks | Id | System |
|---|---|---|---|---|---|---|---|
| /dev/hda1 | * | 1 | 1 | 511 | 163812+ | 6 | DOS 16-bit >=32M |
| /dev/hda2 |  | 512 | 512 | 563 | 16640 | 82 | Linux swap |
| /dev/hda3 |  | 564 | 564 | 1023 | 147200 | 83 | Linux native |
