
+   1. Start with a clean reboot of the Windows 95 virtual machine.
+   2. On the VMware application window, select Settings, VMware Tools Install. Your screen should resemble Figure 7.18.
+   3. If this is your first time installing VMware Tools, you might want to take the opportunity to read the online help when prompted.
+   4. VMware has temporarily mounted a special virtual floppy disk image in the Windows 95 virtual machine. Go to My Computer and double-click the Floppy icon to open the image.
+   5. Double-click the VMware Tools icon shown in Figure 7.19.
+   6. VMware Tools installs with a standard wizard. Accept the default settings shown in Figure 7.20 and proceed with the installation.
+   7. When installation is complete, Windows brings up the Display Properties control panel. Click the Advanced button to reach the Advanced Settings screen. Select the Adapter tab (which should come up by default). You should see a window like the one in Figure 7.21.

![](img/b2b6702758c230ce537468351fc8af15_147_0.png)

Figure 7.18

![](img/b2b6702758c230ce537468351fc8af15_147_1.png)

Figure 7.19 The VMware Tools installer is stored on a special virtual floppy disk.

![](img/b2b6702758c230ce537468351fc8af15_148_0.png)

Figure 7.20

![](img/b2b6702758c230ce537468351fc8af15_148_1.png)

Figure 7.21 The Windows Display Adapter must be changed to the special VMware SVGA driver.

+   8. You need to change the Standard Display Adapter to the custom VMware driver. Click the Change button. You should see only the Standard Display Adapter (VGA) listed, as in Figure 7.22.
+   9. Click Have Disk, and specify the path as A:\win9x. This reads the driver from the VMware Tools virtual disk image.
+   10. Windows finds VMware SVGA(FIFO). Accept this choice.
+   11. Finish the installation wizard. Commit to the change by clicking Close on the Windows control panels.
+   12. Windows suggests a reboot. First, you need to disconnect the VMware Tools disk image, so click Settings on the VMware window and select Cancel VMware Tools Install (see Figure 7.23).

![](img/b2b6702758c230ce537468351fc8af15_149_0.png)

# Figure 7.22

![](img/b2b6702758c230ce537468351fc8af15_149_1.png)

Figure 7.23 Select Cancel VMware Tools Install to detach the virtual floppy disk with the VMware Tools install program.

+   13. Tell Windows to go ahead with the reboot.
+   14. After the reboot, you should notice that Windows is somewhat more colorful and see an icon (a small set of tools) in the Windows system tray.
+   15. You can enter Display Properties and increase the size and color depth of your Windows desktop (limited by the range of your XWindows display) and change the settings in VMware Tools by right-clicking the Tools icon and selecting Main window. See the results in Figure 7.24.

![](img/b2b6702758c230ce537468351fc8af15_149_2.png)

Figure 7.24 The VMware Tools window provides convenient configuration shortcuts.

16. You can safely start using full-screen mode whenever you are in your Windows virtual machine. Click Full Screen at the top of the VMware window, and use Ctrl+Alt+Esc to exit full-screen mode.

## Installing Windows 95 Applications

Although Microsoft includes some applications in the core Windows 95 installation, chances are you want to use software more powerful and exciting than Notepad and Paint. By now, I hope you don’t need my help understanding Windows installation wizards. But for the sake of completeness, a model software installation, along with VMware-specific notes, follows.

In this illustration, I install the Word component of Microsoft Office 97, a good representation of the sort of mainstream application you might want to run in a Windows virtual machine, WordPerfect for Linux notwithstanding:

+   1. Start VMware and boot your Windows 95 virtual machine.
+   2. If you have another CD-ROM in the drive, disconnect VMware from the CD-ROM drive and eject the CD.

> Depending on how CD-ROM access is configured on your Linux system, this step can be something of a chore! You first have to ensure that no open Linux windows, programs, or shells are accessing the CD-ROM. Then, you need to use the Disconnect command under Devices on the toolbar (or use the VMware Tools) to release VMware’s hold on the CD-ROM drive. You might need to type umount /dev/cdrom at a terminal prompt to completely release Linux’s hold on the CD.

+   3. Insert the Microsoft Office 97 CD-ROM.
+   4. Re-connect VMware to the CD-ROM drive. You can do this either by clicking Devices in the VMware toolbar or by using the VMware Tools icon in the Windows tray (see Figure 7.25).
+   5. VMware should spin up the CD-ROM and Windows should automatically launch the Microsoft Office installation program (see Figure 7.26).
+   6. Click Install Microsoft Office to start the setup program.

![](img/b2b6702758c230ce537468351fc8af15_150_0.png)
