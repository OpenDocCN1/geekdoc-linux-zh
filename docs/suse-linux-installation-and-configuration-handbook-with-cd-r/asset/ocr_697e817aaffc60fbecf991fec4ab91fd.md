+   4. Type p to have fdisk show you all the partitions on your hard disk.
+   
+   5. To find where Windows is installed, you should use a line such as this:
+   
+   `/dev/hda2 256 1997 13992615 f Win95 Ext'd (LBA)`
+   
+   From the file system type at the end of the line, you can tell that this is a Windows 9x partition.
+   
+   6. Now that you know the partition you want is /dev/hda2, type q to quit fdisk.
+   
+   You can use LILO to boot this partition.

> TIP
> 
> You can use LILO to boot another installation of Linux. Yes, you can have another partition with SuSE Linux on it and have LILO boot it. In this case, you will need to know the name of the partition on which this second SuSE Linux installation lies. Why would you want to do this? If you want to test something and you are too worried you might corrupt your main SuSE Linux installation, you can have another one to test.

Now that you have the information you need, you can create a new boot configuration for LILO:

+   1. Run YaST in the LILO configuration mode:
+   
+   `# yast --mask lilo`
+   
+   2. Press F4 to add a new configuration for LILO to load.
+   
+   3. In the Configuration Name option, type the name you want to use to load this configuration. For example, if this configuration is going to load Windows 98, a good name might be win.
+   
+   4. Press the Tab key to move on to the Which Operating System option. Here you have three choices from which to pick:
+   
+      - **Boot Linux**—Choose this option if you want to boot another kernel for your system.
+      - **Boot DOS/Win**—Choose this option if you want to boot a Windows- or DOS-based partition. This option should be used if you want to boot any other operating system, including another Linux partition.
+      - **Boot OS/2**—Choose this option if you want to boot OS/2.
+   
+   5. The next option is (Root) Partition to Boot. This is where you specify to LILO the partition to boot. YaST will attempt to guess the correct partition to boot according to what you picked for an operating system. Correct it if it's wrong. (To see a list of partitions that fit your operating system choice, press F3.)
+   
+   6. The Kernel Optional option is activated if you pick Boot Linux. This option is useful if you are testing a new kernel. When you check this option, LILO will never complain if it can't find the test kernel.