# ## 20 Part I: Installing Fedora Core

Defragmenting consolidates all files on your hard drive into contiguous portions. This task is necessary because Windows is a slob as operating systems go, scattering data all over the hard drive faster than a nerd chasing autographs at a Star Trek convention.

These steps show how to defragment your Windows partition:

+   1. Close all programs and windows on your computer, leaving just the desktop and icon bar.
+   2. Double-click the My Computer icon on the desktop.
+   3. Select drive C by clicking it, and then choose File Properties Tools.
+   4. Click the Defragment Now button.

The defragmentation program looks at the drive to determine whether it needs defragmentation.

You may get a message telling you that you don’t need to defragment because your hard drive is not very fragmented; don’t believe it. Under ordinary circumstances, this statement may be true. But resizing a disk is a tricky affair; you must fully defragment your hard drive because you’re going to move the end of the partition file system and make the partition smaller, erasing everything outside that barrier.

+   5. **Click Start.**

The defragmentation window appears and the process begins.

Defragmenting can take a long time, depending on the size of your hard drive and how spread out (fragmented) the data is across the disk.

Click the Show Details button and you can scroll up and down the large window to watch the defragmentation process in action. The colored blocks represent programs and data; the white space represents free space on your hard drive that FIPS can allocate to the Linux file system. The movement of the blocks around the screen shows that the data is being moved forward on the drive. Expect to see white space appear toward the bottom of the window, which represents the end of the data. At the end of the defragmentation process, no colored blocks appear at the bottom of the window, and all the blocks are compressed toward the top of the window. After what may seem like quite a long time, defragmentation ends. All useful blocks of information are now at the beginning of the drive, making it ready for the resizing program.

These instructions describe how to defragment your computer if you’re running Windows NT, Windows 2000/2003, or Windows XP (NTFS):

+   1. Close all programs and windows on your computer.
+   2. Click Start Programs Accessories System Tools Disk Defragmenter.