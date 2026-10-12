# Figure 5-24 Installation Complete

![](bbox=[0.12, 0.19, 0.74, 0.53])

The installation program will prompt you to prepare your system for reboot (see Figure 5-24, Installation Complete). Don’t forget to remove any diskette in the floppy drive or CD in the CD-ROM drive.

After your computer’s normal power-up sequence has completed, you should see LILO’s graphical prompt, at which point you can do any of the following things:

+   Press [Enter] -- Causes LILO’s default boot entry (whichever OS is listed as default) to be booted.
+   
+   Choose a boot label, followed by [Enter] -- Causes LILO to boot the operating system corresponding to the boot label. (Press [?] at the LILO text boot: for a list of valid boot labels.)
+   
+   Do nothing -- After LILO’s timeout period, (which, by default, is five seconds) LILO will automatically boot the default boot entry.

Do whatever is appropriate to boot Red Hat Linux. You should see one or more screens of messages scroll by. Eventually, you should see a login: prompt or a GUI login screen (if you installed the X Window System and chose to start X automatically).