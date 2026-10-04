
# Setting Aside Space (for Fedora Core)

You do need to defragment your hard disk to make room for Fedora Core. What defragmenting does is move all the files to the beginning of the partition and pack them tight. The result is free space at the end of the partition, so the partition can be shrunk without destroying any data.

To defragment the hard disk, follow these steps:

- 1. Double-click My Computer from the desktop, right-click the disk icon, and then select Properties from the pop-up menu.
- 2. In the Properties window, click the Tools tab and then click the Defragment Now button.
- 3. Wait. Wait and wait.

You hear lots of noise from the disk drive while it moves files around. After a couple of hours, the defragmenting completes.

There are some gotchas with these instructions. First, don't use your PC or other programs while defragmenting the hard disk. Close all programs, including ones in the system tray. One good way to do this is to press Ctrl+Alt+Del (which calls the Task Manager), select program you want to stop, and then click the End Task button.

The second gotcha is that the defragment does not move hidden files — plenty of such files are in your system. You don't see them in the folders because (what?) they are hidden. You may have to manually find the hidden files and see whether you can delete the ones that seem to be junk. (Don't worry, a how-to is coming up.)

![](img/d9230b719dc0efd80851f363d8c6f571_61_0.png)

You can find all the hidden files in your PC with a simple command. Open a Command Prompt and type the following commands:

```
cd \
dir /a:s > hidden.txt
```

After the command finishes, you have a list of all hidden files in the text file hidden.txt. Open the file in Microsoft Word or just type edit hidden.txt to view that file in an editor. When I tried this, I noticed a lot of files with names ~WRL0004.TMP — and clearly seemed to be temporary, created by some Microsoft software (probably Word). Why are they hidden? Anyway, I had to change the file attribute using MS-DOS incantations like ATTRIB -H ~WRL0004.TMP and typing ERASE ~WRL0004.TMP to delete the file. But it's worth taking your time and doing it carefully!

![](img/d9230b719dc0efd80851f363d8c6f571_61_1.png)

Another option for dealing with hidden files is to just hide them and then run the defragmenter. To unhide all files in the PC, type the following command in MS-DOS:

```
attrib -h * /s
```

Sit back. After a long time, this command hides all files. Then you can run defragmenter.

# Resizing your hard disk

After defragmenting the hard disk, you're ready to shrink the existing disk partition. You want to partition without damaging the current contents. You have two choices:

- PartitionMagic: This commercial product can resize hard drive partitions and create new partitions for any version of Windows.
- FIPS: This free program runs in MS-DOS mode and can split an existing partition into two. FIPS works only with Windows 95/98/Me. More accurately, FIPS does not work with the NTFS file system that's often used in Windows NT/2000/XP systems. For yours, best bet is PartitionMagic.

# Repartitioning with PartitionMagic

PartitionMagic, from PowerQuest, can resize and split partitions from Windows 95/98/Me to Windows NT/2000/XP. It's a commercial product, so you have to buy it to use. At the time I'm writing this, the price of PartitionMagic is $69.95. You can read about and buy it at www.powerquest.com/partitionmagic.

![](img/d9230b719dc0efd80851f363d8c6f571_62_0.png)

Resizing the partition always involves the risk of losing all data on the hard disk. Therefore, before resize hard disk using a partitioning tool as PartitionMagic, back up your hard drive. After making your backup — before you do anything to the partitions — please make sure you can restore your files.

When you run PartitionMagic, it shows the current partitions in a window. If you're running Windows XP, your hard disk typically has two partitions: one small partition that contains XP installation files, and one huge partition that serves as the C drive. You have to reduce the size of the existing C drive. Doing so creates unused space following that partition. Then, during Fedora Core installation, the installation program can create new Linux partitions in the unused space.

To reduce the size of the Windows partition, follow these steps:

- 1. In the partition map in PartitionMagic's main window, right-click the partition and select Resize/Move from the menu. The Partition dialog box appears.
- 2. In the Resize Partition dialog box, click and drag the right edge of the partition to a smaller size. For a large hard disk (anything over 10GB), reduce the Windows partition to 5GB and leave the rest for Fedora Core.
- 3. Click OK and Apply to apply the changes. After PartitionMagic has made the changes, click OK.
- 4. Reboot the PC.
- 5. Choose Start > Programs > Accessories > System Tools > ScanDisk to run ScanDisk.

You don't have to do anything with the disk left over after shrinking the partition that used to be the C drive. During installation, the Fedora Core installer uses free space to install Fedora Core.

# Repartitioning with FIPS

The DVD-ROM includes a utility program FIPS (First N nondestructive Partition Splitting Program) that can split an existing disk partition into two partitions. FIPS cordons off the unused part of a hard disk and makes a new partition of that unused part without destroying any existing data. FIPS cannot split partitions with the NTFS file system that's often used in Windows/2000/XP systems.

> Some words of caution before you proceed to repartition your hard disk with FIPS. In the words of author Arno Schafer, "FIPS is somewhat experimental although it has been used by many people successfully and without problems." That tells you in a nutshell that you're on your own when it comes to using FIPS. Neither the publisher nor I can accept responsibility or liability for damages resulting from use or misuse of FIPS. There is a chance that FIPS could damage your hard disk, making it unusable. Try FIPS only making sure that you backed up everything on the hard drive and your backup is usable. Also, before you use FIPS, check your hard disk to make sure it's ready:

![](img/d9230b719dc0efd80851f363d8c6f571_63_0.png)

- Your hard drive has only a FAT or FAT32 partition to start with.
- The drive has enough free space available for a useful Fedora Core installation — and that means 3 to 4 gigabytes (3–4GB) of free space.

- The drive must be defragmented before you can use FIPS.
- The drive must not be in use. You can't partition the hard drive while you're using it, which means (among other things) that you can't run FIPS from Windows. You have to shut down Windows, boot from a startup disk, and run FIPS itself.

When you're ready to use FIPS, follow these steps (FIPS only if you are running Windows 95/98/Me):

- 1. Open the Control Panel by choosing Start > Settings > Control Panel.
- 2. Double-click the Add/Remove Programs icon in the Control Panel.
- 3. Click the Startup Disk tab, click the Create Disk button, and follow the instructions.
- 4. Insert your book's DVD-ROM in the DVD-ROM drive.
- 5. Use Explorer to view the contents of the DOSUTILS folder. Then copy FIPS.EXE and RESTORRB.EXE to the startup disk in the A drive.
- 6. Go to the FIPSDOC folder that is inside the DOSUTILS folder on the DVD. Copy the ERROR.TXT file to the startup disk.
- 7. Leave the startup disk in the A drive, and restart the PC.

The PC boots from the A drive and displays the A: \prompt.

- 8. Type FIPS.

The FIPS program gives you an opportunity to save a backup of important disk areas before you. After, FIPS displays the first cylinder where a new partition can start.

- Use the left and right arrow keys to adjust the size of the new partition — the one that results from splitting the existing partition.
