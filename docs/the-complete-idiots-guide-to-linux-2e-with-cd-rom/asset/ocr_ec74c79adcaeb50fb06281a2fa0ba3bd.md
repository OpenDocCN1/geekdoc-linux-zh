as defrag.exe or optimize.exe for this purpose. If not, there are several available from commercial vendors (Norton Utilities is one) that will do the job. Fips is only able to handle DOS and Windows 95-style partitions. If you are running Windows NT or OS2, you might need to take a look at a commercial product like PartitionMagic (see http://www.powerquest.com) that also supports NTFS and HPFS—even Linux drives.

The fips program, along with some readme files you should definitely read before installing, is located on the CD-ROM under col\tools\fips15. Let’s take a quick look at how to repartition your disk space using fips:

+   1. Back up any important data before repartitioning. If something goes wrong, you will lose all your existing data.
+   2. Defragment your system.
+   3. Boot your computer into DOS. (You might need to create a DOS boot diskette; follow your computer’s manuals on how to do this.)
+   4. Insert the Linux CD-ROM into your computer. If your boot diskette does not enable use of the CD-ROM, you might have to copy the fips program to another diskette.
+   5. If your CD-ROM is located on drive D, at the prompt type d:col\tools\fips15\fips.exe. If your CD-ROM is accessible by another letter, substitute it for the correct drive.

Follow the onscreen instructions to reserve the amount of space you expect to need for Linux. A good estimate should include allowances for the size of your Linux install (usually 418MB), the size of your swap space (same size as your memory), and extra space for data you create while using Linux (usually a few hundred megabytes). To resize your DOS partition, use the arrow keys on your keyboard. Press Enter to set the appropriate size. Confirm your changes and reboot your computer.

# Installing Linux

How you install Linux will depend on whether your BIOS supports booting from a CD-ROM. If your computer’s BIOS doesn’t support booting from a CD-ROM, you’ll have to create two floppy disks: One disk will be a boot disk, and the other will be a modules (drivers) disk.

If your computer supports booting from a CD, you can skip building the floppies; go directly to the section “Starting the Install.”

# Building the Boot and Modules Floppies

If your computer doesn’t support booting from a CD-ROM device, you’ll need to create two floppies that start the Linux installation. One disk is required to boot the computer (the boot disk). The other disk (the modules or drivers disk) will contain additional software that is necessary if you

+   - Need access to a PC card (PCMCIA device support) while installing. (Maybe you are using a PCMCIA network or SCSI card or some other peripheral.)