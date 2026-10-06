# APPENDICE A Creating a Linux Installer on Flash/USB Devices 779

9. The completed dialog box on our sample system is shown next. You can see that we selected a Fedora-Server-DVD-x86_64_LATEST.iso image file to be written to a target device labeled USB-DRIVE to which Windows assigned the drive letter G:

![](bbox=[0.296, 0.193, 0.704, 0.503])

10. Click the Create Live USB button to start the process.

11. When the process completes, close the Live USB Creator window. You may now unplug the flash/USB device and insert it into the appropriate port of the new system that you want to install the Linux distribution on.

12. If necessary, configure the BIOS or the UEFI of the target system to boot off the flash/USB-based device. Once booted into the installer, follow the installation steps as described in Chapter 2, or as specified by the distro vendor.

# Ubuntu Installer Using UNetbootin on Windows

UNetbootin is the Swiss Army knife—of universal bootable flash/USB devices. It is supported on multiple platforms—Linux, and Mac OS X. It has built-in support for bootable flash/USB versions of all the popular Linux distros (as well as not so popular ones). It even supports esoteric utilities (such as FreeDOS, Super Grub, Parted Map, BackTrack, NTpasswd, Ophrack, and so on) that often come handy for System Administration tasks. As an added bonus, UNetbootin is a stand-alone executable and does not need to be installed before using it.