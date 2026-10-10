
![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_146_0.png)

**Figure 5.1** Click on the Defragment Now button on the Tools tab of the Properties dialog box to begin defragmenting your notebook's drive.

Click on the Defragment Now button to defragment your notebook's hard drive. This will ensure that your data is placed at the beginning of the hard drive prior to partitioning.

## Using FIPS

Every Linux distribution comes with the DOS-based FIPS partitioning utility. You'll usually find FIPS under the /dosutils directory on your Linux CD-ROM, or you can download the latest version from the FIPS home page (see the “Resource Information” section at the end of this chapter).

> **Note:** Before you partition your notebook's hard drive, be sure to back up all important documents and directories. Although partitioning is quite safe until changes are written to disk, you should take basic precautions before partitioning. You have been warned!

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_146_1.png)

Using FIPS is easy. First, insert a blank diskette into your notebook and create a bootable DOS system disk by using the DOS **FORMAT** command with its /s option:

```bash
format /s a:
```

Next, copy the **FIPS** command, along with the **RESTOREB** command and the file **ERRORS.TXT**, to the floppy. The **RESTOREB** command may be used to restore the Master Boot Record (MBR) of your notebook's hard drive. Reboot with your new disk, and then run the **FIPS** command like this:

```bash
A:\>FIPS
```

The **FIPS** command will then check your notebook's hard drive to find a bootable partition. You'll see a table of your notebook's drive information, such as that shown in Figure 5.2.

Figure 5.2 shows a notebook that has a single 1GB hard drive with a DOS file system residing in the first partition. To start partitioning, press any key. FIPS will continue checking your drive and will report on the drive's characteristics.

> **Warning:** If you see an existing partition equal to or double the size of your notebook's RAM, do not attempt to split or change that partition! The partition probably uses your notebook's suspend-to-disk area (as supported by your notebook's BIOS). Leave that partition alone when partitioning or installing Linux, or you might have a real hassle on your hands when you try to reinstall or reconfigure the partition!

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_147_0.png)

You'll then be asked if you want to make a backup of your drive's MBR. This is not important when installing Linux, because you'll most likely install the LILO boot loader into the MBR, and in this example, you can simply restore the MBR by using the DOS **FDISK** command like this:

```bash
A:\>FDISK /MBR
```

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_147_1.png)

**Figure 5.2** *The FIPS command will check your notebook's drive before partitioning.*

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_148_0.png)

**Figure 5.3** Use the left and right cursor keys to adjust the size of your new partition when using FIPS.

If you choose to back up the MBR, type a y. Otherwise, type an n and press Enter. You’ll then be asked to use the right and left cursor keys to assign a size to the new partition, as shown in Figure 5.3.

The original partition’s size will be on the left side of the screen. As you use the cursor keys, you’ll see the size of the new partition decrease or increase. FIPS will automatically try to offer a new partition using as much free space as possible, so be sure to leave room for your original operating system. When finished, press Enter. You’ll see the display shown in Figure 5.4.

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_148_1.png)

**Figure 5.4** The FIPS command will display your hard drive’s new partition table before writing it to your hard drive.

Figure 5.4 shows that FIPS displays a new partition table, with the new partition offering 950MB for Linux. Type `c` to continue, and FIPS will create the new partition. If you re-run FIPS, you can continue to create other partitions. However, this step is unnecessary and can be done during your Linux installation.

## Apple's Drive Setup

Installing Linux on the Apple iBook requires that you use Apple's Drive Setup command, preferably on an external drive, to create non-HFS or HFS+ partitions in AUX format. You can install Yellow Dog Linux on the iBook's internal drive; however, you'll first need to create room for Linux by following these basic steps:

- 1. Reboot your iBook with your Mac OS Install CD (by holding down the C key).
- 2. Use the Apple Drive Setup utility's Custom Setup button to reformat your iBook drive with an HFS (not HFS+) partition and an unallocated partition.
- 3. Reinstall the Mac OS or use your Restore CD.

Note that early iBooks came with only a 3.2GB drive, but newer models sport a 6.4GB drive. On the 3.2GB model iBook, you can safely allocate 1.5GB for the Mac OS HFS partition, do a full restoration, and still have 800MB left over for additional applications or data. However, if you perform a full installation of Yellow Dog Linux on the unallocated 1.5GB partition, you'll end up with less than 100MB free space left on the Unix partition. If you need more room for both operating systems, you'll need to upgrade the internal hard drive on your iBook. If you need more room for Linux, install only a minimal Mac OS, and do not perform a full restoration.

## Partitioning Problems

Problems can occur when you partition your hard drive. Many of the problems you can run into when using FIPS are detailed in documents under the dosutils/fipsdocs directory on your Linux CD-ROM. Here are some documents you might want to read if you have problems:

- **fips.doc.** Section 10 details troubleshooting problems.
- **fips.faq.** Contains frequently asked questions, including common problems.
- **special.doc.** Discusses using FIPS with OS2, OnTrack Manager, and DOS compression utilities.

Technical information regarding FIPS is in the file techinfo.txt.

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_150_0.png)

## Step-by-Step Installation of Red Hat Linux

This section details a step-by-step installation of the latest version of Red Hat Linux. As you know by now, there are many different ways to install Linux and different Linux distributions. This section details one way to install Linux—by booting using a boot disk with an inserted CD-ROM.

The easiest way to install Linux is to boot directly from CD-ROM. You'll need to make sure your notebook's BIOS supports booting from CD, and that the CD-ROM device is listed as the first device, as shown in Figure 5.5.

You'll generally find boot images included on your Linux CD under the /images directory. To quickly create a boot disk using Linux, mount the CD, insert a blank floppy disk, and use the Linux dd command like this:

```bash
# mount /mnt/cdrom
# dd if=/mnt/cdrom/images/boot.img of=/dev/fd0
```

This will create a boot disk. You can then reboot to perform your installation. If you're using DOS, use the RAWRITE command (found under the /dosutils directory) to create your boot disk.

### Installation

When the installer boots, you'll see the first installation screen, as shown in Figure 5.6.

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_151_0.png)

**Figure 5.6** Use the installation dialog box’s boot options to designate a type of installation.

When installing Red Hat Linux, you can choose from a variety of installations, such as text or expert. If you do nothing for a short period of time, the installer will boot directly to the installation. The text installation method is handy for situations in which your notebook’s display adapter might not work correctly with Red Hat’s graphical installation interface. The expert installation offers finer controls to aid in configuring your notebook’s hardware to work with the installer. You’ll also see a rescue mode that may be used to help you boot and restore an existing installation.

Press Enter to begin the installation. The screen will clear, and you’ll see the display shown in Figure 5.7.

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_151_1.png)

**Figure 5.7** Choose a language for your installation.
