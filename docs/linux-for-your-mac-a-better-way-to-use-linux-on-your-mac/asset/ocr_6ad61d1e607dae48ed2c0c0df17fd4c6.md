Double-click the file `yaboot.conf` inside the System Folder on your HFS boot partition. Using the SimpleText editor, look for:
```
...
default = LinuxPPC Installer
...
```
Change this entry to:
```
...
default = Boot LinuxPPC -- Ultra safe video
...
```

Save your changes, and then quit the application. Go to the **Apple menu**, select **Control Panels**, **Startup Disk**. Click to select the boot partition in the **Startup Disk** dialog box, and then choose **Restart from the Special menu**.

The screen clears, the **LinuxPPC 2000 Q4** splash menu appears, and you reboot to Linux. If you want to reboot to Mac OS, press the spacebar. When the desktop icons appear, use the cursor keys to navigate to the **CD-ROM** icon (make sure there is no CD-ROM in your computer), and then press Enter. You reboot to Mac OS. After booting to Mac OS this way, you again have to use the **Startup Disk** control panel in order to reset your computer to boot to Linux.

# # Installing SuSE PPC Linux

This section details an installation of SuSE PPC Linux 7.1. Insert Disk 1 from the **SuSE PPC CD-ROM** set, and then reboot your computer. Hold down the e key to boot from the CD-ROM. If you cannot boot from the CD-ROM, boot to Mac OS, open the **Blueboot** folder on the CD-ROM, and then double-click the **BootX** app. When **BootX** appears, click the **No Video** check box and click the **SuSE Linux** button to launch the installer.

Linux boots up on your computer while Tux the penguin dances. Be patient while the installer goes through initial hardware detection. When the screen clears, you are presented with a dialog box that asks you to choose a type of install using `yast` or `yast2`. Use the Tab key to navigate the cursor through the dialog boxes. Use the up and down arrow keys to scroll. Press Enter after highlighting a desired button or menu item.

Try the `yast2` graphical install. If the screen clears and the `yast2` dialog box appears, you can proceed. Your mouse may also be recongnized and functional. If `yast2` fails, reboot and use `yast`. The rest of this install describes the graphical install.