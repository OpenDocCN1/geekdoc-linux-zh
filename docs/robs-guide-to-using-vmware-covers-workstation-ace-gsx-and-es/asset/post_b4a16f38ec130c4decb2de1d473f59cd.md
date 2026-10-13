
## 9 Optimizing your Virtual Machine Environment

This chapter contains useful tips for optimizing the performance of your virtual machine, and to make your virtual environment easier to work with.

### 9.1 Performance Tips

A few basic tips can help you experience better performance in your virtual machines. First, make sure that you always install the VMware tools (especially for Windows), because together with the SVGA display driver, the performance when using the guest operating system is much better.

- Disconnect the CD-ROM device

If your guest operating system is trying to access the CD-ROM or DVD player, (either because you inserted a CD-ROM, or because the OS or an application is trying to read data from a CD-ROM that is not there), that process could slow down the host and guest.

When your virtual machine is completely configured and the OS is installed, go to the virtual machine settings and set the CD-ROM device not to Connect at power on.

![](img/25fe75b93b97a021effaba85db112a52_132_0.png)

Figure 9.1: Configure CD-ROMs as not connected by default.

- Run in full screen mode

In Windows, but especially in a Linux host working in the graphical environment is much faster if you run your virtual machine in full screen mode.

- **Disable visual effects and other unneeded features**

Windows contains a lot of features that enhance the user's experience. But all of that costs in performance level and uses resources from the display environment. Turn off this functionality (if you can do without it) in your virtual machine. You can find these effects in the Display Control Panel.

- **Remove hardware that you don't need**

It will not increase your performance dramatically; however, if you remove devices that you do not need from your virtual machine, such as the sound adapter and the USB bus, it will prevent your guest from playing sounds that will be processed by the host's sound card. Also, it will not attach USB devices to the virtual machine that it will start to access.

- **Use a second hard drive in your host**

If you will be running multiple virtual machines on your host system, you can increase the performance by using multiple hard disks. Remember from the VMware introduction that both the host and the guest are accessing their data on the same physical disk. Therefore, splitting them up or running virtual machines from different hard disks will increase performance, especially in the case of running disk intensive applications within your guest operating systems.

- **Use a separate disk for your swap files**

Just as with a real PC, it is a good idea to have a separate swap partition for your OS. Of course, the best thing is to prevent swapping in the guest operating system as much as you can, by assigning enough memory to the virtual machine. This is an advanced topic that you might want to investigate for your specific environment; however, if for example the guest needs virtual memory (swap space) you could create a fixed sized disk that holds the swap file. Also, make sure that the file is not defragmented on your host system.

There is also another reason to use a separate swap file disk that I find is more important for efficient use than for performance. If you assign a virtual disk that will grow dynamically to your virtual machine for use as a swap disk, you will see that it will become a large file. If you want to archive the virtual machine, this swap file space can be easily reduced by replacing it with an empty disk. To prepare this, I have created a swap file on an NTFS partitioned virtual disk, which I have copied to a safe location on my hard disk. If I am going to archive the virtual machine in a ZIP-file or if I need to burn it on a CD-ROM or DVD, I replace the used swap disk with this empty one. This way it does not take up space in the archive copy.

This method also keeps the virtual disk smaller which makes it more efficient to shrink your disks.

### 9.2 Shrinking your Virtual Disks

Owners of multiple 400 GB hard disks in their PCs can skip this paragraph. Others, for whom hard disk space is limited, must read on to find out how they can save valuable disk space.

Your virtual hard disk files will grow dynamically. They start with a few megabytes but could become very large. After installing an operating system, your hard disk could be well over 2 GB, even if the OS you have installed only takes 1 GB of disk space. There are several reasons why your virtual disk will grow more than you would expect. During installation, for example, temporary files are copied to the hard disk, sometimes being unzipped locally. After that they are copied to the correct location on your hard drive and your temporary files are deleted again.

The installations of service packs, patches, and software applications will also work with temporary files on your virtual hard disk, causing your virtual disk to grow larger and larger. Dynamically growing disks are not automatically shrunk in size. Your virtual machine will re-use space available in the virtual disk file, but in the end your virtual disk file will grow larger than you need it to be.

The shrink process itself should start preferably from the VMware tools Properties window in your guest operating system.

Figure 9.2 is from a Windows guest, but the same window and options are available for NetWare and Linux.

![](img/25fe75b93b97a021effaba85db112a52_134_0.png)

Select the disks that you want to prepare and click Prepare to shrink. This process will take from a few minutes to half an hour depending on the size of your virtual disk, and of course the performance capability of your host's hard disk.

Figure 9.2: Virtual disks must be prepared for shrinking.

Tip: You can shrink your disks from the command line with the Virtual Disk Manager. This is discussed in section 7.3: "Using Virtual Disk Manager".

When the prepare for shrinking process is complete, you are asked if you want to run the shrink operation at that point. If you click yes, VMware will start to create a temporary file that it will use during the shrink process. You will need to have at least as much hard disk space available as what your virtual disk is using on your hard disk, before the shrink operation is complete.

> Tip: For all operating systems it is a good idea to remove unnecessary files from the guest operating system's hard disk. Remove large files, temporary files, etc. Specific tips on Windows and NetWare can be found in chapter 9.

### 9.3 Archiving your Virtual Machines

Working with VMware is very efficient, because you do not need extra PCs and a new PC with a new operating system is up and running in less than an hour. If you are working with new PCs with the same operating system repeatedly, you will find that it is useful to have a working copy of a virtual machine with that OS, which you can start with. This section will provide you with a few tips to work even more efficiently with VMware.

Archiving virtual machines is not only about storing them on a safe location to use them later, but also to have a copy that you can use as your starting point for future projects. The method described here also helps you save your virtual machine on one or more CD-ROMs or DVDs.

> Tip: For virtual machines that will contain a large amount of data use virtual disk files that are split up in 2 GB parts. That will make it easier to archive the files on multiple CD-ROMs (zipped per file) or DVDs.

#### Remove snapshots

Before archiving your virtual machine, remove the snapshot you have taken. The original .vmdk file will be untouched and extra s###.vmdk files are created. Together, they will take up more disk space than actually in use by the guest operating system.

#### Shrink your disks

Use the shrink process described in the previous paragraph to decrease the size of your virtual disk. If you have chosen to use a separate disk for the swap file for your guest operating system, you can now also replace that .vmdk file (with an original smaller one) and save it in a safe location.

#### Power off your virtual machine

Do not copy or ZIP your virtual machine in a suspended state. It would work if you resume the virtual machine on the same PC with the same version of VMware. Resuming the virtual machine on another PC, with a different CPU in the future or with a newer version of VMware, will most likely result in error messages. Also, you have to discard the saved memory state file (VMSS) anyhow.
