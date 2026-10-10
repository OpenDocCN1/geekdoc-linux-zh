# 64 Installing SUSE Linux

| Select This Item | To Do This |
| :--- | :--- |
| Installation — Safe Settings | Disable potentially troublesome features, such as ACP1, APM (Advanced Power Management), and DMA (direct memory access) for IDE interface, and start installing SUSE. Select this option if the installation hangs with any of the other options. |
| Rescue System | Start a small Linux system in memory so that you can troubleshoot by logging in as **root** |
| Memory Test | Check to see if there is any problem with the PC's memory |

**Table 2-2 (continued)**

Along the bottom of the SUSE installer boot screen, you see some information about using function keys F1 through F6. Table 2-3 explains what each of these functions does.

You can also provide other installer options — as well as Linux kernel options — at the Boot Options text box below the boot menu. The *installer options* control some aspects of the installer’s behavior, whereas the *kernel options* are passed to the Linux kernel that starts when you start the installation. I explain many of these boot options in Chapter 3 of this minibook.

| Press This Function Key | To Do This |
| :--- | :--- |
| F1 | Get context-sensitive help — help information that relates to the currently selected item. Use the up- and down-arrow keys to read the Help screen and the left- and right-arrow keys to jump between topics. You can dismiss the Help screen by pressing Escape. |
| F2 | Select the language and keyboard mapping to be used by the boot loader. |
| F3 | Select a screen resolution that you want the YaST installer to use for its GUI. If the GUI screen fails to appear, you can select Text Mode for a text mode interface. |
| F4 | Select the source from which you want to install. The choices are: CD or DVD; or network sources with different protocols, such as FTP, HTTP, NFS, and SLP (Service Location Protocol). |
| F5 | Update a driver module for new hardware for which drivers may not be on the CD or DVD. You will be prompted to insert the updated driver module on a floppy disk or CD-ROM disk after you start the installation. |

# Table 2-3 Using Function Keys at the SUSE Installer Boot Screen

![](bbox=[0.15, 0.86, 0.25, 0.92])

The installer initially picks a rather high screen resolution for the GUI screen (typically, 1280 x 1024 pixels). You should press F3, which brings up a menu from which you can select a more reasonable screen resolution, such as 1024 x 768 pixels.