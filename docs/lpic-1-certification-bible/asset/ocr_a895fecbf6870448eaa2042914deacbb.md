Choose the hard disk you want to partition. Depending on your system configuration you may need to heed the warning in the LILO Limitations screen, as shown in Figure 1-23. As discussed previously in this chapter, some systems cannot boot if the Linux kernel is stored beyond the 8GB barrier on a hard disk, or past cylinder number 1023. New versions of LILO allow you to boot from any point on the drive, if your system has a BIOS that is new enough. If your system does not support this, or if you are just unsure, make a /boot partition below the 8GB barrier.

![](bbox=[0.18, 0.3, 0.87, 0.5])

# Figure 1-23: LILO Limitations screen

Debian uses `cfdisk` to handle partitioning. Set up your partitions as you see fit. For lab purposes it is probably a good idea to split up your volumes so you get experience with more than just single volume systems. A good method for splitting the disk is to put /home, /tmp, and /var on separate partitions. You can also put /usr on a separate partition, but be sure to give it at least a gigabyte of disk space so you have room for software installations later. Don’t forget to make a swap partition!

Once cfdisk is completed, you will be prompted to initialize the swap partition(s), as shown in Figure 1-24.

Any time you initialize a new partition in the Debian install you will be prompted to perform a bad block check. This writes some data to every sector on the disk and then reads it to make sure it is the same. If the read data is different, then the sector is marked as bad. Modern disk controllers can now handle bad blocks automatically, and as this process can take a very long time, you can normally skip this test. But, if the hardware is older or questionable, it does not do any harm to run the test. After the test you can confirm the disk initialization, which will destroy any data. Figure 1-25 shows the bad block test screen.