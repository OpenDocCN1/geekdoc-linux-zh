![](bbox=[0.22, 0.09, 0.9, 0.44])

Figure 18-1: Mounting a Windows partition in Nautilus

# 18A-2: Unmounting Your Windows Partition

You can unmount your Windows partition immediately after finishing your work with it, or you can just wait until you shut down your system, whereupon it will be automatically unmounted. Before you can unmount it yourself, you must first make sure that none of your programs is accessing files or folders on the partition. Nautilus and the Terminal are the usual suspects, so before unmounting, close any Nautilus or Terminal windows that are browsing that partition. Once you’ve done that, click the little eject icon next to the Windows partition in the side pane of a Nautilus window (Figure 18-2), or right-click it and select Unmount.

![](bbox=[0.25, 0.7, 0.38, 0.8])

Figure 18-2: The Windows partition "OS" in the Nautilus side pane, complete with eject icon

# Accessing a Linux Partition While Running Windows

Viewing your Windows files in Ubuntu isn’t too stressful, as you have no doubt just found out. But what about going the other way and getting Windows to recognize your Linux partition? Unfortunately, Windows isn’t too helpful in this respect—it can only view FAT or NTFS-format partitions and has no built-in support for the ext format normally used by Linux. As such, if you need access to your Linux files in Windows, it’s probably easiest to create a separate FAT partition to be shared between both operating systems (see Appendix C). Hmmm, not exactly convenient.