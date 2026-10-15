All right, enough studying. You now know plenty about VMware theory—certainly enough to take the plunge and actually install it on your PC. So get out the book’s included CD (if you haven’t already) and let’s get started!

# Installing from the Included CD

This book comes bundled with a CD-ROM that contains, among other things, the core VMware binaries. It should take only a few minutes to install VMware from the CD-ROM, and after visiting the VMware Web site to request a free 30-day trial license, you can start running guest operating systems on your Linux PC.

Earlier versions of VMware sometimes required users to download a special version of the XFree86 server, and you might find some reference to this requirement in VMware documentation. But recent versions of XFree86 (which you should have installed, if your system meets the requirements outlined in Chapter 3, “Equipping Your PC for VMware”) eliminate this problem, and you shouldn’t need to worry about it.

+   1. If you haven’t already, log in to Linux and start XWindows with the user account you will use for running VMware.
+   2. Open a terminal window.
+   3. Insert the VMware CD-ROM, and mount it as you normally would if your system does not automatically mount newly inserted CDs (usually by typing mount /dev/cdrom).
+   4. The CD contains a directory called VMware Binaries, which contains the VMware installation program. cd to this directory off the mountpoint used by your CD-ROM drive. (Often it is cd "/mnt/cdrom/VMware Binaries". Quotes are necessary because the directory contains a space.)
+   5. Copy the file VMware-2.0.1-570.i386.rpm to a working directory on your hard drive.

> If your system does not support RPM package installs, copy the file VMware-2.0.1-570.tar.gz instead, and watch for modified instructions ahead.

+   6. If you do not normally run as root (yes, all the books tell you not to, but some people still do it!), you need the root password and the ability to use the su (superuser) command.

![](bbox=[0.05, 0.85, 0.18, 0.95])