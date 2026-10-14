# Virtual computer

A virtual computer is effectively an entire PC recreated in software. The virtual computer boots, just like a normal computer, and an operating system can be installed within it. The virtual computer's hard disk is contained within a file in the "host" filesystem. Once up and running, the "guest" operating system's desktop appears within a program window.

The free-of-charge VMware Player application allows easy virtual computing, and is ideal for trialing Ubuntu. Here are the steps required:

+   1. Head over to www.vmware.com/products/player and download VMware Player. Install it once downloaded. Then head over to www.ubuntupocketguide.com/vmware.html and download an empty virtual computer container zip file.

+   2. Extract the contents of the virtual computer zip into a new folder and copy the Ubuntu ISO image file you downloaded earlier into the same folder. Rename the ISO image as ubuntu.iso.

+   3. Start the virtual computer by double-clicking the startubuntu file in the new folder (you may see startubuntu.vmx, but it is the same file).

+   4. From this point onward, follow the instructions under the Standard (Repartitioning) heading above. When you come to the partitioning stage, you'll only see one option: Guided—Use Entire Disk. This is fine.

> NOTE Remember that you're installing Ubuntu onto a virtual hard disk, that is actually a file within your Windows filesystem. You aren't about to wipe the computer's real hard disk!

Once installation has finished, Ubuntu will "reboot" within the virtual computer—you don't have to reboot the real computer! When you've finished using Ubuntu, just quit VMware like you would any other program—the virtual Ubuntu installation will be suspended until you next start VMware by double-clicking the startubuntu file again.

Note that you'll need to click the mouse in the VMware window to switch keyboard and mouse input into the virtual operating system. Once this happens, the mouse cursor will be "locked" within the window. To free it, hit the Ctrl+Alt keys together.