# Chapter 9 ◆ Configuring the System with YaST

This module is in the System section of the YaST menu, or it can be started from the command line with the command yast2 floppy. You are simply asked which floppy you want to create. The choices are as follows:

+   * Standard Boot Floppy 1
* Standard Boot Floppy 2
* Standard Boot Floppy 3
* Rescue Floppy
* Modules Floppies
* Custom Floppy
* Download Floppy Image

These do exactly what they say they do: Create the floppy disks from images on the installation media. YaST will use whatever installation source has already been set up to write the floppy disks. Whoever of the ones you choose, you are prompted for the floppy device (typically /dev/fd0), and the disk is written out to the floppy. There is an option to format the disk. If you choose Modules Floppies, you are prompted for which one you want to create. Usefully, the menus tell you which floppy supports hardware. There is more information in the files /boot/modules1.txt, /boot/modules2.txt, and so on for the installation media.

If you want to use the floppies that you have created to start an installation or the rescue system, just boot from the first boot floppy. Depending on your hardware, you may be prompted for one or more of the modules floppies. If you choose the rescue system at the initial boot, you will be prompted for the rescue floppy.

> If you want to run the rescue system from the set of floppies, all three boot floppies and possibly the modules floppies have been inserted, you will receive a message similar to “Make sure that CD is in your drive.” Instead of OK, choose Back, select your language settings, and then select rescue system. You will be prompted for either the CD or the rescue floppy.

# Setting Up Proxy Settings

If your company uses a proxy, or you use a proxy at home, you can create a global proxy that a large proportion of network utilities will try to honor.

You can set up an anonymous proxy or one user with credentials. The proxy configuration itself is not intelligent because all it does is inform your applications that the proxy should be a certain host with a username and password (if specified). It does not impact how the application communicates with the server.