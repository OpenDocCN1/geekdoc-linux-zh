# Part I: Getting Started with Ubuntu

FIGURE 2-17
Creating a USB startup disk

![](bbox=[0.095, 0.169, 0.658, 0.483])

When starting up from this disk, documents and settings will be:
* Stored in reserved extra space
How much: 1.0 GB
Discarded on shutdown, unless you save them elsewhere

+   3. Verify that the USB disk partition upon which you use area to create a bootable Ubuntu system is listed and highlighted in the USB disk to use in the middle of the dialog. The line below the USB disk list identifies whether the selected USB partition has sufficient space for installing a bootable system. If the USB stick that you are using is not formatted, click Format to format it. Once formatting completes, you will see two entries in the "Disk to use" section — one for the stick itself, and one that ends with a number, identifying a specific partition on that. Make sure that the entry you want is selected.

+   4. To create a bootable USB stick that supports the persistent storage of applications that you install, files and directories that you create, and system configuration information, make sure that the "Stored in reserved extra space" radio button is selected at the bottom of the dialog shown in Figure 2-17. Drag the slider below this radio button to identify the amount of space that you want to allocate for storing persistent data.
If you do not want to create any persistent storage, click the "Discarded on shutdown" radio button. If you select this radio button, your bootable USB stick will behave exactly like an Ubuntu Desktop CD. Any files or directories that you create, applications that you install, and application and system configuration information that you modify will not be preserved when you shut down a system that you have booted from the USB stick.