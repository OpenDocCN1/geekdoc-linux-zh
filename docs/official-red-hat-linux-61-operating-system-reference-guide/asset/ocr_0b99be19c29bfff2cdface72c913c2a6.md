Ready to write new partition scheme to disk
Do you want to proceed (y/n)?

Answering **y** completes the resizing operation. A harmless error message may occur, stating, in effect that FIPS cannot reboot the system.

After a successful operation, the disk will have two partitions. The first partition (hda1 or sda1) will be used by Windows. We recommend that you start Windows (remember to remove the boot disk from drive A:) and run scandisk on drive C:.

If you encounter any problems, (for example, Windows will not boot), you can reverse the FIPS resizing operation with the restorb.exe command, which you copied to your DOS boot disk. In case of any errors, read the FIPS documentation files (fips.doc and fips.faq), which indicate a number of factors that could cause the resizing operation to fail. If all else fails, you can restore Windows with the backup you made.

The second partition (hda2 or sda2) contains the space that the Red Hat Linux installation program will use. When the Disk Druid screen appears during installation, delete this partition (the installation manual explains how), then proceed with Linux partitioning.