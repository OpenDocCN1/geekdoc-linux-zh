That said, if you decide to repartition your hard drive with FIPS, it is vital that you do two things:

+   - Perform a Backup -- Make two copies of all the important data on your computer. These copies should be to removable media (such as tape or diskettes), and you should make sure they are readable before proceeding.

+   - Read the Documentation -- Completely read the FIPS documentation, located in the FIPS directory on Red Hat Linux CD-ROM.

Should use decide to use FIPS, be aware that after FIPS runs you will be left with two partitions: the one you resized, and the one FIPS created out of the newly freed space. If your goal is to use that space to install Red Hat Linux, you should delete the newly created partition, either by using fdisk under your current operating system, or while setting up partitions during a custom-class installation.

The following instructions are a simplified version of the FIPS documentation file, fips.doc, located in the FIPS directory (/dosutils/fips20/*). These instructions should apply in most instances. If you encounter any problems, see the documentation file.

+   1. From Windows:

+   - Do a full backup.

+   - Run scandisk to verify that the hard drive contains no bad clusters.

+   - Decide how to distribute the available space on the hard drive between the operating systems. Use Windows Explorer to see the free space on the drive. Make a note of the space (in megabytes) that each operating system will have.

+   - If you don't have one, create a DOS boot disk.

To create a DOS boot disk, first boot your machine to DOS.

Next, insert a blank, formatted diskette into the floppy drive.

Type the following at the command prompt and press [Enter]:

```
FORMAT A: /S
```