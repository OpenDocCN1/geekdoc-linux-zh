

![](img/48d064407ff591f0b5365c2d2919ee6e_31_0.png)

Figure 1-3. Installing Ubuntu inside Windows.

7. In the username text field, type a username you want to use within Ubuntu. Wubi will suggest a username based on your Windows login details, but you can type something different.

8. In the password fields, type the password you'd like to use for your Ubuntu login account. A good password involves letters, numbers, symbols and even spaces, and is as long as possible.

9. Once done, click the INSTALL button. There are two stages to the installation. First, the container files are created within the Windows filesystem (if you're using the standalone Wubi installer, the Ubuntu files are also downloaded; this may take some time). The computer then reboots for the full installation to take place. Upon rebooting, you should select Ubuntu from the boot menu—use the up/down cursor keys, and hit Enter when Ubuntu is highlighted.

Once installation has completed, you can boot into Ubuntu by selecting it each time at the boot menu.

Now skip to the next chapter to learn how to configure Ubuntu.

> TIP It's possible to convert a Wubi installation into a full hard disk installation. It's a little complicated, however, so you might like to try it when your skills improve. Instructions can be found at http://wubi.sourceforge.net/lvm.html.

## Virtual computer

A virtual computer is effectively an entire PC recreated in software. The virtual computer boots, just like a normal computer, and an operating system can be installed within it. The virtual computer's hard disk is contained within a file in the "host" filesystem. Once up and running, the "guest" operating system's desktop appears within a program window.

The free-of-charge VMware Player application allows easy virtual computing, and is ideal for trialing Ubuntu. Here are the steps required:

- 1. Head over to www.vmware.com/products/player and download VMware Player. Install it once downloaded. Then head over to www.ubuntupocketguide.com/vmware.html and download an empty virtual computer container zip file.
- 2. Extract the contents of the virtual computer zip into a new folder and copy the Ubuntu ISO image file you downloaded earlier into the same folder. Rename the ISO image as ubuntu.iso.
- 3. Start the virtual computer by double-clicking the startubuntu file in the new folder (you may see startubuntu.vmx, but it is the same file).
- 4. From this point onward, follow the instructions under the Standard (Repartitioning) heading above. When you come to the partitioning stage, you'll only see one option: Guided—Use Entire Disk. This is fine.

> NOTE Remember that you're installing Ubuntu onto a virtual hard disk, that is actually a file within your Windows filesystem. You aren't about to wipe the computer's real hard disk!

Once installation has finished, Ubuntu will "reboot" within the virtual computer—you don't have to reboot the real computer! When you've finished using Ubuntu, just quit VMware like you would any other program—the virtual Ubuntu installation will be suspended until you next start VMware by double-clicking the startubuntu file again.

Note that you'll need to click the mouse in the VMware window to switch keyboard and mouse input into the virtual operating system. Once this happens, the mouse cursor will be "locked" within the window. To free it, hit the Ctrl+Alt keys together.

## Problematic installations (alternate install)

Sometimes Ubuntu's installation program goes wrong. Most commonly, this results in graphical problems that mean the installer program doesn't work correctly.

In situations such as this, you can use the alternate install CD. This can be downloaded from www.ubuntu.com as an ISO image, just like the main install CD (click the link marked "Text-based alternate installer installation disk", and, after selecting a download location near you, choose the file whose name ends with -alternate-i386.iso).

The alternate CD provides the same version of Ubuntu as the main install disc, but uses a "text mode" installer that doesn't have a graphical interface. As such the installer is compatible with virtually all computers, but this comes at a price because it isn't as user-friendly as the main Ubuntu installer. The terminology can be obtuse for beginners, and the lack of a graphical interface means no mouse—you must navigate around the interface using the keyboard.

Here are the steps needed to use the alternate install CD:

- 1. Assuming that you've downloaded the CD and burned it to a blank CD-R/RW disc, as described earlier, boot your computer using the disc. Follow Step 1 under the Standard (Repartitioning) heading to ensure your computer boots from the CD-R/RW disc.
- 2. At the boot menu, choose your language and select the Install Ubuntu menu option.
- 3. When the installer starts, follow the initial installation steps by highlighting a choice on-screen using the cursor keys, and hitting Enter. In most cases, the default choices are fine. At one stage the installer will attempt to go online, and might report an error. Don't worry about this. If you're prompted for wireless network details, just select not to go online (select "Do not configure the network at this time").
- 4. Eventually you'll be prompted for a hostname. This is how the computer is referred to on the network. The default is fine.
- 5. As with the main installer, the alternate installer will attempt to resize the Windows partition. Hit Enter when offered the Guided—Resize SCSI1 option (or Guided—Resize IDE1).

