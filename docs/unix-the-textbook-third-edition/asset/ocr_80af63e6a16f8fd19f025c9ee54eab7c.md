website given. On our Windows system, we downloaded PCBSD10.2-RELEASE-x64-desktop.ova.

+   2. If you double-click the .ova file on a Windows system, it will automatically open the image for you in the default virtualization application, which we assume here is VirtualBox.

+   3. The first time a PC-BSD .ova file is opened on a Windows system, a screen will open so that you can review the VM's settings that came with the file. Depending on the settings, you can either type in the desired value or select it from a drop-down menu. Once you are finished, click the "Import" button. It will take a few minutes for the import to complete and a status bar will indicate the status of the import. Once imported, the VM will show in the left-hand frame of VirtualBox. Highlight the VM and click "Start" to boot into the image.

+   4. When using the "desktop" edition download of PC-BSD, the VM will boot into the postinstallation configuration screens so that the system can be configured, as shown in Section 23.2.3. Once the display wizard is finished and the login menu appears, input the username and password that you configured at the "Create a User" screen.

+   5. Use PC-BSD. When ready to shut the PC-BSD system down, use the techniques shown in Section 23.2.5.3, "Graceful Shutdown." When PC-BSD completely shuts down, you are returned to the VirtualBox VMM.

+   6. To delete the PC-BSD guest VM, make the VirtualBox VMM menu choice "Machine>Remove" when the PC-BSD guest VM is highlighted. In the dialog box that appears, if you make the choice "delete all files", be aware that the .ova file is retained!

# EXERCISE 25.10

Use the methods shown in Section 25.4.5.2 to install a PC-BSD guest on a Windows or LINUX system of your choice.

# 25.4.5.3 Installation of a Solaris Guest on LINUX and Windows Hosts

This section shows the procedure for installing a Solaris guest VM in a LINUX or Windows host running VirtualBox. The techniques shown here work for both LINUX and Windows systems.

The minimum requirements on the LINUX or Windows host are:

+   X86 system with a minimum of 4 GB RAM.

+   A minimum of 4 GB free disk space is needed for initial installation.

+   The available space on the virtual disk can grow to a maximum of 64 GB.

+   VirtualBox is already installed.