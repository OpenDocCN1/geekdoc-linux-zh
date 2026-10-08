your system does not support bootable DVD/CD-ROMs, you will have to set up an alternative boot method such as a USB disk with **diskboot.img** or a PXE server.

+   - You can create a bootable DVD/CD-ROM disk with which to start the installation. The DVD/CD-ROM boot disk image is located in the **images** directory and is called **boot.iso**. You can also use this disk to install from alternate sources such as a hard drive or a network location such as an NFS, FTP, or Web site.

+   - With the **diskboot.img** file (also in the **images** directory) you can boot from small USB drives or any bootable device large enough to hold the 2.6 kernel (the size of the **diskboot.img** file, about 6 MB). This is a VFAT file system. Check first if your system can boot from the USB drive.

+   - You can also boot from the PXE (Pre-Execution Environment) server using the **initrd.img** file in the **images/pxeboot** directory. A PXE server operates through DHCP and TFTP servers off a Linux system. Check the PXE documentation file, **pxelinux.doc**, in the `/usr/share/syslinux-2.11` directory (version number may differ).

If you are installing from a Fedora DVD-ROM, you will need a DVD-ROM drive on your computer to read the DVD-ROM disk. If your system supports bootable DVD/CD-ROMs, then it will boot from this DVD-ROM, letting you install your Fedora system from the DVD-ROM directly.

# Install Methods

Fedora supports various methods for installation. Other than the graphical install, you can user a text install or a low-resolution (lowres) graphical install, which is helpful if your graphics card was not correctly detected. If you have difficulty with detecting your hardware, you can use the noprobe option, which will let you provide your own drivers, or the expert option, which will let you choose all your hardware. You may also need to use **nofb** for some LCD monitors, or set **acpi=off** to disable ACPI if it stops your installation.

For text installs, you would add these options at the boot prompt. If you are using the graphical menu, as would normally be the case, press the TAB key to display the command line listing your current options. Add in the one you want. Use backspace to delete current options. Press the esc key to return to the menu.

+   - **linux text** Use a text-based install interface employing a text cursor to make selections with the arrow, TAB, and ENTER keys.

+   - **linux lowres** Use a low-resolution graphical interface that is video card independent.

+   - **linux nofb** Disable the frame buffer (needed for some LCD monitors like Dell).

+   - **linux noprobe** Do not probe hardware.

+   - **linux acpi=off** Turn off ACPI, which can interfere with the install procedure.

+   - **linux expert** Select all hardware.

+   - **linux askmethod** Select a method of installation, as from a hard disk or a network site.

+   - **linux vnc** Start a VNC install from a VNC site.

+   - **linux ks=file*location** Start an automated install using a kickstart configuration file.