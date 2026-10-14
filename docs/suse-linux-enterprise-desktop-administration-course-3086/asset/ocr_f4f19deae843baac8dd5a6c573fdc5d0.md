You should not confuse auto installation with cloning or imaging. An automated installation is a regular installation where answers to questions asked during the installation are contained in the control file. The hardware detection is still done so that the same control file can be used on diverse hardware. Imaging or cloning generally requires the source and target of the image to have identical hardware.

AutoYaST is optimally used in conjunction with an installation server that is also providing a TFTP and a DHCP server. This setup has the following advantages:

+   - To start the installation, you only have to insert a suitable boot disk. If you are using PXE boot-enabled network interface cards, not even a boot disk is required.
+   - The computer receives all information necessary for the installation via the network.
+   - Even on-site attendance of an administrator is unnecessary for the installation if the network card supports Wake on Lan.

The installation server can be accessed via the NFS, HTTP, and FTP protocols. This results in a highly simplified installation of a large number of individually configured computers.

AutoYaST can also be used to copy additional files to the installed system and can include scripts that are executed at the end of the installation.

You can create a control file at installation time. In the last menu of the installation process, you can check the box Clone This System. This will create an autoinst.xml file in the home directory of the root user (/root). The creation of an AutoYaST control file using the YaST AutoYaST module is covered later in this section.

# Objective 3—The Configuration File for AutoYaST

The easiest way to create a configuration file for AutoYaST is to use the YaST Autoinstallation module. Select Computer > More Applications > yast2 > Miscellaneous > Autoinstallation, or log in as root and enter yast2 autoyast in a terminal window.

This module starts with the dialog shown in Figure 15-1. The left part of the window contains all parameters that can be configured in a treelike structure. If you select a main entry, all available modules of this entry are displayed in the main part of the window. To select a module, either select the link in the main window or the name of the module in the left window.

![](bbox=[0.1, 0.75, 0.28, 0.87])

You do not need to configure every single aspect of the machines to be installed, because the automated installation makes use of the hardware-detection capabilities of YaST. For example, you do not need to provide the type of network card because the hardware detection will take care of this.

To configure an item, select the underscored line in the main window. Selecting Configure opens the same YaST configuration dialogs as those you see when installing or administering SUSE Linux Enterprise Desktop 10. However, the configuration information is written to the AutoYaST control file. Nothing is changed on the installation you work on.