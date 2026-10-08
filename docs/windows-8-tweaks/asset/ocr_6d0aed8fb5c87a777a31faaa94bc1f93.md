# # Installing from USB

The Windows 8 retail versions include installation software on a DVD. That works fine for the majority of users, but it is a big problem for those who own laptops, tablets, or other computers without optical drives. If you don’t have an optical drive on your computer, you need to take some extra steps to install Windows 8.

A few solutions to this problem exist, such as PXE (Preboot Execution Environment) network booting to a Windows Deployment Server (a feature of Windows Server 2008 and newer). However, the most popular and easiest to configure is a bootable USB flash drive. This is my personal preference as well, because installing Windows 8 from a USB flash drive is actually much faster than installing from a DVD.

You need a 4 GB USB flash drive to have enough space to fit the entire Windows 8 installation code on the drive. I found that the 4 GB SanDisk Cruzier works well for booting the Windows 8 installation code and seems to be compatible with a wide range of computers. However, just about any 4 GB USB flash drive should work these days.

If you have physical media rather than a digital download ISO file, the instructions for creating boot media are slightly different. Follow the instructions relevant for your situation.

# ## Creating the USB Boot Media from a Physical DVD

This section is pertinent if you have access to a Windows PC, XP or newer, because you need DiskPart to be able to create the USB boot media.

Before you begin it is important to understand that any data on your USB flash drive used to create the boot media will be permanently deleted because the process reformats the drive. Save any important documents to another location before proceeding to the next section.

# ### Preparing the USB Flash Drive

The partitioning and filesystem on the USB flash drive are important for booting. Only one partition can be on the device, it must be set to active, and the filesystem must be FAT32. Many computers with the new UEFI BIOS replacement have problems booting USB flash devices with any filesystem other than FAT32. Insert the drive into a Windows computer and follow these steps:

+   1. After the drive has been recognized and installed on the computer, click the Start button, type **DiskPart**, and hit Enter.
2. In the DiskPart window, type **list disk** and hit Enter as shown in Figure 2-1.
3. Locate the Disk # of your USB flash drive. You can easily find it by looking at the size column. Once you have the ID, type **select disk #** and hit Enter. (Replace # with the actual disk ID, such as 1.)