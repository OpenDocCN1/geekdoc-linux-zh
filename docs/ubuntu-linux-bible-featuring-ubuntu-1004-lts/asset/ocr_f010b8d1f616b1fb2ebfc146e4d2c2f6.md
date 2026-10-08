# FIGURE 24-8
Specifying the type of virtual disk to create

![](bbox=[0.105, 0.175, 0.703, 0.413])

This dialog provides two options for the type of virtual disk that you want to create, either a dynamically expanding image or a fixed-size image. The differences between these two are as follows:

+   * Fixed-size image: All of the disk space required on your host system for the virtual disk is immediately allocated when you create the new virtual disk, based on the disk size that you will specify in a subsequent dialog

+   * Dynamically expanding image: Dynamically expanding images initially use the minimum amount of disk space on the host system that is required to hold the files you've installed in your virtual machine, plus some extra space required to hold information about the filesystem(s) that the virtual disk contains. For example, the 20-GB dynamically expanding disk image for a Microsoft Windows 2003 Server actually uses only 2 GB after a complete, default system is installed. If you install additional applications and as the virtual machine creates and adds additional files for caching, logging, and so on, the dynamically expanding image will continue to grow, up to the maximum size that you will specify in a subsequent dialog.

These two different types of disk images have some performance implications for your virtual machine and the host system:

+   * Fixed-size image: Using a fixed-size disk image will result in slightly higher performance for your virtual machine and the host system because neither of them needs to allocate additional space for the disk and to the housekeeping required to accurately track the disk blocks on the host system that are actually allocated to the virtual machine. If you know that you will be installing large applications or creating/downloading large files in a virtual machine, you may well pre-allocate all of the disk space because you're probably going to grow it eventually. On the down side, your host system will have less storage