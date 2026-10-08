The BIOS also acts as a main hardware component control panel, where low-level settings for all your hardware devices are made. The device boot order, port addresses, and feature settings such as plug and play are all located in the BIOS setup screens. For example, if you want to change the order of the drives that your computer checks to boot from, you want to modify the device boot order. I have to modify this setting almost every time I install Windows, because I want my computer to boot off the CD-ROM to launch the install DVD instead of booting of the operating system on my hard drive.

BIOSes typically are unique for each PC model and vendor. Some PCs come with a newer version of BIOS called UEFI that is more efficient but managed the same way. Accessing the BIOS on a PC is also unique to each PC vendor. Nevertheless, the most common way to access the setup screen is to press F1, F2, or the Delete key when the POST screen is displayed. Some computers even tell you which key to press to access the setup screen, as my notebook does. If your PC doesn’t allow you to access the setup screen in this way, consult your computer documentation or contact your computer manufacturer for instructions.

> **NOTE** While you are making changes in the system BIOS, make sure you do not accidentally change any other settings. If you accidentally change the value of a setting and do not know what to change it back to, just exit the BIOS setup screen as the on-screen directions indicate and select Do Not Save Changes. Then just reboot and re-enter the setup screen and continue hacking away at your system.

# # Changing the Boot Order of Your Drives

Most computers are set up so that when you first turn them on, they check to see whether to boot from drives other than your hard drive. The BIOS automatically checks to see whether you have a bootable disc in your CD/DVD drive. Then, after it has checked all possible locations for a boot disk, the system defaults to your hard drive set in the BIOS and starts booting Windows.

What is the benefit of changing the boot order of your system devices? If you modify the order of the boot devices so that the hard disk with Windows installed is searched first by the BIOS, the system does not have to waste time checking other devices for boot records. Just by changing the order of the devices, you can shave anywhere from one to several seconds off your boot time, depending on the speed of your hardware and number of drives your system has installed.

To change the boot order (or sequence, as some call it), you have to enter the system BIOS setup screen that was mentioned previously:

+   1. Press F1, F2, F8, Delete, or the correct key for your specific system on the POST screen (or the screen that displays the computer manufacturer’s logo) to enter the BIOS setup screen.
2. Look for where it says Boot, and open the submenu.