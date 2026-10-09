When you select the radio button labeled **Guess keymap** and click **Guess**, ubiquity leads you through a series of questions and, based on your answers, tries to determine which type of keyboard you are using. Click **Forward** when you are satisfied with the result.

When you select the radio button labeled **Choose your own**, ubiquity activates the two list boxes below these words. Select a **country** and keyboard type from these list boxes and click **Forward**.

# ## Prepare Disk Space

The Prepare disk space screen controls how **ubiquity** partitions the hard disk. See page 36 for a discussion of the issues involved in partitioning a hard disk.

# ## Guided Partitioning

With a single, clean hard disk—a hard disk with nothing installed on it, as it comes from the factory (i.e., no partition table)—the **ubiquity** partition editor displays a Prepare disk space screen similar to the one shown in Figure 3-7. In this case, the simplest way to partition the disk is to allow the **ubiquity** partitioner to do it for you. This technique is called *guided partitioning*. By default, the radio button labeled **Erase and use the entire disk** is selected and the name of the only hard disk in the system is displayed in the drop-down list below these words. If the system has two or more hard disks, you must select from this list the disk where you want to install Ubuntu. Click **Forward**. The **ubiquity** partition editor creates two partitions on the hard disk: a small swap partition (page 37) and a root partition (/, page 37) that occupies the rest of the disk.

The **ubiquity** partition editor does not partition the disk at this time. At any time before you click **Install** on the Ready to install screen, you can change your mind about how you want to partition the disk. Click the button labeled **Back**. You may have to back up through several screens to display the Prepare disk space screen again, but you can then set up the disk the way you want it.

See “Advanced Guided Partitioning” on page 70 for information on using the other selections in the Prepare disk space screen.

# ## Migrate Documents and Settings

If you are installing Ubuntu on a system that already has one or more operating systems installed on it, and you are not overwriting those operating systems, the Migrate documents and settings screen displays a list of accounts and settings from the existing operating systems. For example, if you are creating a dual-boot system on a system that already has Windows installed on it, this screen shows the accounts from the Windows system and a list of programs and settings. It might show your name from the Windows system and, under that, Internet Explorer and My Documents. Put ticks in the check boxes adjacent to those items you want to migrate to the Ubuntu system. On the lower portion of the screen, enter the information necessary to create an Ubuntu user to receive the migrated information. Click **Forward**.