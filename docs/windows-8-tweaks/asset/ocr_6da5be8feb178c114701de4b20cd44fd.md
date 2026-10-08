+   4. Type **clean** and hit Enter to destroy any partitions, file systems, and data that may currently be on the device.
5. Now it is time to create the partition. Type **create partition primary** and hit Enter.
6. For booting it is important to set the partition as active. Type **active** and hit Enter.
7. As I mentioned earlier, the filesystem must be FAT32. Type **format fs=fat32 label=win8boot quick** and hit Enter. This performs a quick format and labels the drive in one step.
8. Type **exit** to close DiskPart. Your USB flash drive is now prepared for the next phase.

![](bbox=[0.11, 0.35, 0.86, 0.66])

# ## Copying the Installation Software

The final step, now that you have your USB flash drive prepared, is to copy the code. If you are a super geek you can use some fancy xcopy or robocopy commands for this step, but this simple copy-and-paste procedure works just fine.

Insert the DVD media into your PC and navigate to the drive on your computer that has the Windows 8 installation files. Select all the files, as shown in Figure 2-2, and then right-click and select Copy.

Navigate to the root of the USB flash drive, right-click and click Paste. The file copy can take a number of minutes, but after it is finished you can install Windows 8 quickly and on machines that don't have an optical drive.