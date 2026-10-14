# Using YaST to Configure LILO

YaST offers a very simple-to-use interface to configure LILO. To fully utilize the interface, you have to be familiar with its various options. Run YaST, navigate to System Administration, Kernel and Boot Configuration, LILO configuration. You can have YaST load directly into the LILO configuration screen by typing the following:

```
# yast --mask lilo
```

Figure 9.1 shows the LILO Installation screen that appears when YaST is loaded. Let's walk through the options on this screen to understand them; use the Tab key to cycle through them.

FIGURE 9.1
LILO setup using YaST.

![](bbox=[0.25, 0.42, 0.78, 0.68])

The first option is called Append-Line for Hardware Parameter (look ahead to Figure 9.2). When the kernel loads, it attempts to auto-detect the configured system resources used by most of the hardware. This can be the Ethernet card, the sound card, and so on. If the kernel is unable to automatically detect the resources used by these devices, you can tell the kernel what these resources are. To do so, you put them here, and when LILO boots the kernel, it will pass them to the kernel. Which parameters you put here depends on the device you are trying to configure.

The next option is Where Do You Want to Install LILO. You get the following four options here:

+   - Master Boot Record—This will make LILO the first thing executed after the BIOS. This is recommended for most configurations because you can configure LILO to give you the option of which operating system to boot.
+   - Boot Sector of the Root Partition—This will place LILO on the boot sector of your root partition. This way LILO should be called by another boot manager. You might want to use this if you are using another boot manager, such as the NT Loader, to boot Linux. Remember, you will always need to use LILO to load Linux.
+   - Boot Sector of the /boot Partition—This will do the exact same thing as the previous option, but will install LILO on a partition you created for the /boot directory.
+   - On Floppy Disk—This will install LILO on a floppy disk. This disk is good for emergencies because you can use it to boot your PC.