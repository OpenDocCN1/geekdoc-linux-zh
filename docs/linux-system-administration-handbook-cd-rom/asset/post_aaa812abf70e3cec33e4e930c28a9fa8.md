
## D.3 Problems Using Very Large Hard Disks

- Create and label a modules diskette:
Write the modules diskette image to a 1.44-MB floppy.
In Linux, use a command such as

```
dd if=modules.img of=/dev/fd0H1440
```

or
```
cat modules.img >/dev/fd0
```

From DOS, use the WRITE3 command and follow the prompts to transfer MODULE.IMG to a floppy.

- Put the installation diskette in your floppy drive and restart your computer.

## Using Problems Using Very Large Hard Disks

Using very large hard disks in PCs can lead to problems because of the limitations of the BIOS and IDE standards on which most PCs are based. Problems arise because the BIOS can manage only hard disks with a maximum of 256 heads, 63 sectors, and 1024 cylinders because the IDE standard is based on a model that specifies the Cylinders, Heads, and Sectors of the hard disks (CHS model), but only allows a maximum of 16 heads, 255 sectors, and 65536 cylinders. The lowest limits of both of these combine to give a maximum size for standard hard disks of 504 MB (16 heads, 63 sectors, and 1024 cylinders).

The newer Enhanced-IDE (EIDE) standard avoids this limitation by not using the CHS model. Instead, a Logical Block Addressing model is used (LBA). This model numbers all sectors on the disk sequentially.

Newer BIOS versions overcome the 504-MB limitation by using an Extended CHS model that extends the maximum number of heads to 256. The new upper size limit, from the Enhanced IDE and Extended CHS models, is almost 7.9 GB.

Linux does not use the BIOS to access your hard disk, so IDE and EIDE hard disks should not cause problems on Linux systems. If problems occur, Linux might be obtaining incorrect disk size parameters from the BIOS. To correct this problem, use boot parameters to pass the correct information to Linux. The parameter totopass "hdx=cyl,heads,sect," where hdx is the hard disk device (hda, hdb, hdc, hdd). More information is provided below on using these parameters to create cylinder counts of less than 1024.

## SCSI Hard Disks

In general, all SCSI hard disks use the LBA mode mentioned above. SCSI hard disks do have a separate problem that EIDE hard disks do not have, however. SCSI hard disks larger than 1 GB must have special treatment with the “fdisk” utility and while configuring the LILO boot manager. If Your SCSI hard disk is affected by this problem, “fdisk” will display messages regarding the problem when you prepare your hard disk. The expert mode of “fdisk” can be used to correct the SCSI problems. The LILO problems are fixed by adjusting the “etc/diskstab” file. Both of these fixes are described below with example.

## Why the Problem Arises

The problem with these larger hard disks is that the partition table must be read before any operating system becomes active. The partition table is accessed via the BIOS, which is limited to 256 heads, 63 sectors, and 1023 cylinders. Because of this, the hard disk controller attempts to convert (or translate) the true parameters of hard disks with more than 1023 cylinders into values that can be accepted by the BIOS.

The partition table itself can always be found at the first cylinder, first sector, and first header (which is the same in any translation); because of this translation from the controller, if all data for the boot process (such as the boot loader and operating system kernel) are not found in the 1024 cylinders, the BIOS cannot successfully boot the system.

Partitions can be created above 1024 cylinders, but you cannot boot these partitions because boot data in those high partitions cannot be accessed until after the system is booted. This only causes trouble when a system has multi-operating systems, and the user attempts to choose which to boot.

A work-around solution is to create a small Linux partition below 1023 cylinders that can be used to boot the Linux system. This partition can be as little as 15 MB, because it only needs to contain the kernel and the root filesystem. The “usr” directory and other information can be stored in a second Linux partition located above 1024 cylinders. Use the “fdisk” utility of another operating system such as OS/2 to create these partitions. Then use the Linux “fdisk” during installation to mark the partitions as Type 0x83, Linux.

## Using Problems Using Very Large Hard Disks

A better solution is to enter the correct combination of cylinders, sectors and heads that the hard disk controller is passing to the BIOS. Use the "fdisk" expert mode, as described below. The following diagram shows an example of the translation of the physical values of the hard disk to LBA direct block addressing, which is finally used by the operating system to access the hard disk.

On the left, you can see that the physical layout of the hard disk is very different from the logical (LBA) values reported. Most hard disks have significantly fewer heads than externally reported. The logical values reported by the hard disk should conform to the limitations of IDE or BIOS. In the case of an EIDE or SCSI controller, the controller itself will do another translation.

SCSI hard disks are usually reported as 64 heads and 32 sectors, giving a size of 64*32*512 Bytes = 1 MB per cylinder. EIDE*32*255 heads. The last translation is done by the operating system. Linux uses Logical Block Addressing (LBA) to refer to the blocks sequentially from the first block to the last block on the hard disk.

Many controllers use different models in order to provide cylinder numbers under 1024. In most cases, the controller first tries to double the number of heads. If this does not result in a cylinder count less than 1024, the controller increases the actual values for heads and sectors to the maximum possible. Overlap between partitions is therefore minimized because each partition begins and ends on a cylinder boundary. The translation by an Adaptec controller of a 4-GB disk gives a count of 255 heads, 63 sectors, and 522 cylinders. Your task is to find out the translation the controller is doing and enter the values for the hard disk into the expert mode of "fdisk." As you do, remember that the total size of hard disk must remain constant. For example, assume that we have a computer with a 4-GB SCSI hard disk. This is more than 1024 cylinders, so "fdisk" gives a warning during installation: the number of cylinders for this disk is set to 4095. This is larger than 1024, and may cause problems with:

1. software that runs at boot time (e.g., LILO)
2. booting and partitioning software other OS (e.g., DOS, OS/2)

When you use the “p” command to display the partition table, you see a sequence of error messages:

| Device | Boot | Start | End | Blocks | Id | System |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/sda | | 1 | 754 | 771088 | 6 | DOS 16-bit-32M |
| /dev/sdb | * | 97 | 1954 | 122892 | 82 | Linux swap |
| /dev/s3 | | 1274 | 1954 | 2456 | 514080 | a5 | BSD/386 |
| /dev/s4 | | 2362 | 2456 | 4095 | 167872 | | Extended |
| /dev/s5 | | 2362 | 2707 | 257008 | 83 | Linux |
| /dev/s6 | | 2394 | 2707 | 642288 | 83 | Linux native |
| /dev/s7 | | 2402 | 2770 | 3436 | 682731 | 6 | DOS 16-bit-32M |
| /dev/s8 | | 2487 | 3436 | 4095 | 674698 | 6 | DOS 16-bit-32M |

Partition 1 does not end on cylinder boundary: phys=(95, 254, 63) should be (95, 63, 32)
Partition 2 does not end on cylinder boundary: phys=(248, 254, 63) should be (248, 63, 32)
Partition 3 does not end on cylinder boundary: phys=(312, 254, 63) should be (312, 63, 32)
Partition 4 does not end on cylinder boundary: phys=(521, 254, 63) should be (521, 63, 32)

To correct these errors, new values must be entered by “fdisk” to the partition boundaries match the values returned by the hard disk and controller. In this example, the 4-GB hard disk shown has 64 heads, 32 sectors, and 4095 cylinders, for a total capacity of 64*32*4095 bytes = 4095 MB.

If you set the number of heads to 255, and number of sectors to 63 (a hint that this value is correct in the error messages shown above), the partition must still have 4095 MB. So if 255*63*cylinders = 4095 MB, then the number of cylinders will be 522.

These new values must be entered into “fdisk.” First, you must change to the expert mode with the “x” command; and then enter the new parameters for the heads, sectors, and cylinders. In expert mode the commands “c” (cylinders), “h” (heads), and “s” (sectors) can be used. Using the calculation above, these values should be 255 heads and 63 sectors.

NOTE: If you are using DOS on your system, never enter a head count of 256. This value will cause DOS to crash without.

Below is how the screen might look like as you enter the new values in “fdisk.”

```
Expert command (m for help): h Number of heads (1-256): 255
Expert command (m for help): s Number of sectors (1-63): 63
Warning: Setting sector offset for DOS compatibility
Expert command (m for help): c Number of cylinders (1-65535): 822
```
