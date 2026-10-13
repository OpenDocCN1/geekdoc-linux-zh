service packs you are planning to use, at this point and run Windows Update to get your machine updated with the latest software and patches.

Tip: At the point, before adding new hardware or patches to the machine, take a snapshot of where the machine is installed. This way if one of the new components breaks, in your Windows environment, you can easily switch back to the point where it all worked fine.

# Windows XP and Server 2003 Activation

Microsoft introduced a mechanism with Windows XP that is now also implemented in Windows Server 2003, where you have to activate Windows. This process generates a checksum based on the hardware in your PC, and uses that to activate Windows via the Internet or via a telephone dialog with a Microsoft representative. If you change pieces of the hardware, Windows will recognize that it is running on a different hardware and requires you to re-activate Windows. You will have to keep that in mind, if you are installing hardware into a Windows XP workstation. You will be reminded by VMware about this with the following dialog box.

![](bbox=[0.05, 0.5, 0.7, 0.65])

Figure 4.1: Install Windows completely before activating your copy.

Adding a single piece of hardware is not a problem, but if you activate Windows before finishing the installation, it could require you to re-activate even before you are finished. So, make sure that you have all your disks configured, that the amount of memory is set to what it needs to be, and that extra network or sound adapters are added before you activate your copy of Windows.

# 4.3 Installing your First Linux Guest

Linux is available in many different distributions, but the installation procedure is similar for almost any of the distributions and uses a CD-ROM or DVD. There are Linux operating systems that you can install over the Internet and as I mentioned earlier, a virtual machine is just like a normal PC, so if you could do it from a hardware box you can also do it from a virtual box.