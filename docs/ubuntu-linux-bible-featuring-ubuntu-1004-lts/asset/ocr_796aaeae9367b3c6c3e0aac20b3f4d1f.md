# # Installing VirtualBox Guest Additions

The open source edition of VirtualBox provides enhanced drivers for better video resolution and better control of mouse interaction in Windows and Linux virtual machines once a virtual machine of either of those types has been installed. These drivers are known as the VirtualBox Guest Additions—you're familiar with VMware, these are equivalent to VMware's Guest Tools.

# Note

The Windows drivers in the Guest Additions are precompiled. Installing the Linux drivers from this package requires the GNU C Compiler (gcc) and the header files for the Linux kernel installed in your virtual machine. See Chapter 23, "Software Development on Ubuntu," for information about installing these in an Ubuntu virtual machine (if you're running some other Linux distribution in your virtual machine, that system's Package Management tools to install the gcc and kernel headers packages for that.).

+   - To install the Guest Additions into a virtual machine, select the Devices Guest Additions menu in a virtual machine. You will see a dialog to effect that the Guest Additions CD image cannot be found on your machine, and you would like to download it over the Internet? Click Yes. If you see a confirmation dialog for the download ("are you sure?"), you should also click Yes, and you will see a download progress bar appear in the bottom-left corner of the virtual machine window as the image is downloaded.

Once the ISO image for the Guest Additions is downloaded, VirtualBox displays a dialog if you want to mount the ISO as a CD drive. Click Yes.

If your virtual machine is running some version of Windows, the Autorun.inf script on the CD will automatically install the Guest Additions for you when the CD is mounted. Running Linux, you will have to start a Terminal window (xterm, GNOME Terminal, Konsole, etc.), mount the image, and run the VBoxLinuxAdditions.script via sudo to build and install the enhanced drivers.

Once you've installed the drivers, you can unmount the ISO image by using the standard mechanism for your operating system, or by selecting the Devices Unmount CD/DVD-ROM menu command from the virtual machine.

# # Starting and Stopping Virtual Machines

Once you've created one or more virtual machines and installed an operating system in each, you can start any virtual machine by selecting its entry in the left pane of the VirtualBox window and ways:

After you're finished using a virtual machine, you can shut it down in one of two ways:

+   - By invoking the standard shutdown process for the virtual operating system that your virtual machine is running. When the shutdown process completes, the virtual machine