# ### Playing Audio CDs with WorkMan

Solaris doesn't come with a utility to play audio CDs, as do the Windows and Macintosh operating systems. However, you can add that capability by installing WorkMan, a third-party freeware utility. You can download a package for WorkMan or an archive for the files you compile from WorkMan's home page at www.midwinter.com/workman/. To install WorkMan, see the section “Packages” in Chapter 12, “Working with File Utilities.”

Once the WorkMan package is properly installed, it will work with Volume Management to mount audio CDs and put on your screen a graphical CD Player. You will first need to attach either external speakers or headphones to your CD-ROM drive to hear the sound.

To attach external speakers or headphones to WorkMan, follow these steps:

+   1. Log in as a superuser at the command line (enter su).
+   2. Install the WorkMan package as described in Chapter 12.
+   3. Edit the `/etc/rmount.conf` file to add the line `action cdrom action_workman.so <path>/workman <options>`.
+   4. Insert an audio CD into your CD-ROM drive.
+   5. Open a Terminal window and enter **workman** at the command line.

The WorkMan utility shown in the following graphic offers you volume and audio controls. You can also create and manage play lists using this program. If you close WorkMan, the audio CD will continue to play, but you can also use this Utility to eject audio CDs.

![](bbox=[0.44, 0.63, 0.66, 0.88])