As instructed, put a formatted disk into your PC's A drive and then press Enter. That disk will become the Red Hat install boot disk.

+   4.  When you see the command prompt again, take the Red Hat installation boot disk out of the A drive and (if you haven’t done so already) label it or mark it so you know what that disk is, and put it aside.

# # Setting Aside Space for Red Hat Linux

In a typical Windows PC, Windows is sitting on a big partition, taking over the whole disk. You want to shrink that partition and create room for Linux. During Linux installation, the installation program uses that free space for the Linux partitions.

The challenge is to resize the current partition without destroying anything on the hard disk. I cover tools that help you resize the partition, but first you have to make sure that all used areas of the disk are contiguous, or as tightly packed as possible. This is where defragmenting comes in.

# ## Defragmenting your hard disk

“Defrag your disk” is the magic chant of many a help desk. It’s the help desk’s prescription for all PC ailments. Well, for once they’re right — you do need to defragment your hard disk to make room for Red Hat Linux. What defragmenting does is move all the files to the beginning of the partition and pack them tight. The result is free space at the end of the partition, so the partition can be shrunk without destroying any data.

To defragment the hard disk, follow these steps:

+   1.  **Double-click My Computer from the desktop, right-click the disk icon, and then select Properties from the pop-up menu.**

+   2.  **In the Properties window, click the Tools tab and then click the Defragment Now button.**

+   3.  **Wait. And wait. And wait.**

You’ll hear lots of noise from the disk drive while it moves files around. After a couple of hours, the defragmenting should be complete.

There are some gotchas with these instructions. First, don’t use your PC or other programs while defragmenting the hard disk. Close all programs, including the ones in the system tray. One good way to do so is to press Ctrl-Alt-Del (which calls up the Task Manager), click which program you want to stop, and then click the End Task button.

The second gotcha is that the defragmenter does not move hidden files — and there are plenty of such files in your system. You don’t see them in the