are installing from the live CD, you won't be able to choose the software to install (in this or the next step) because the entire contents of the CD are installed to hard disk.

+   *   **Installation Categories** — If you are installing from DVD, select each category that appears to see which groups of software packages are installed. Then select the Optional packages button to add or subtract packages from each group.
+   *   **About to Install** — Up to this point, you can quit the install process without having written anything to disk. When you select Next, the disk is formatted (as you chose) and selected packages are installed.

> NOTE: After answering the questions, the actual installation of packages from the DVD takes between 20 and 60 minutes, depending on the number of packages and the speed of the computer hardware. For the live CD, the installation process is typically much faster because the contents of the CD are simply copied to hard disk.

When installation is done, remove the Fedora DVD and click Exit to reboot your computer. If you installed from the live CD, reboot your computer and remove the live CD before it's time for the installed system to boot. Linux should boot by default. After Linux boots for the first time, the Fedora Setup Agent runs to let you read the license agreement, set system date and time, configure your display, check your hardware, add a user account, configure your sound card, and install additional CDs. On subsequent reboots, you will see a login prompt. You can log in and begin using your Linux system.

If you need more information than this procedure provides, go to the detailed installation instructions just ahead.

# Detailed Installation Instructions

This section provides more detail on installation. Besides expanding on the installation procedure, this section also provides information on different installation types and on choosing computer hardware.

If anything goes wrong during installation and you get stuck, go to the “Troubleshooting Installation” section at the end of this chapter. It gives suggestions for solving common installation problems.

> CAUTION: If, when installing Windows or Fedora, you find that the other operating system is no longer available on your boot screen, don't panic and don't immediately reinstall. You can usually recover from the problem by booting the live CD that comes with this book, and then using the grub-install command to reinsert the proper master boot record. (You can also enter rescue mode by selecting **Rescue installed system** from the Fedora DVD boot screen.) Refer to the “Using the GRUB boot loader” section later in this chapter. If you are uncomfortable working in emergency mode, seek out an expert to help you.