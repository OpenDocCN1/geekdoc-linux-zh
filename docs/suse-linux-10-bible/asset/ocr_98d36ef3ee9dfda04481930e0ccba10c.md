# Chapter 9 + Configuring the System with YaST 223

To load the GUI YaST interface, type yast2 (as user root) at the command prompt. YaST detects that X is running, it runs the GUI. If not, it runs the text-based interface. If you want to use the text-based interface, use the su command to become the root user and type yast at the command prompt.

When loaded, you will see the main YaST menus, in Figures 9-1 and 9-2, depending on what version of the interface you have chosen.

From now on we deal with the GUI-based YaST system.

# YaST Modules

The YaST system is split into seven menu topics, each opening up another list of menus for direct configuration of the chosen module.

> If you want to load a YaST module without loading the main menu, you can enter yast2 modulename. For a list of modules available in your installed YaST environment, type yast2 -l.

![](bbox=[0.136, 0.403, 0.193, 0.458])

The available topics for YaST configuration are as follows (with the YaST name in brackets to load directly with yast2 modulename):

+   * Software

+   * Control the installation and removal of software packages (sw_single).
* Update your SUSE system to the latest patch from the SUSE servers (online_update).
* Add a SUSE installation source (FTP, HTTP, SAMBA, directory, and so on) (inst_source).
* Use a patch CD to update your system (online_update .cd default).
* Install SUSE into a directory (dirinstall).
* Install INTO into directory for Xen (xen-dirinstall).
* Media check (test SUSE CDs or DVDs) (checkmedia).
* Change the characteristics of your system (package defaults, system language, and so on) (update).
* UML installation (install a User Mode Linux instance) (umi).

+   * Hardware

+   * Configure Bluetooth (bluetooth).
* Configure CD/DVD mount points, and so forth (cdrom).
* Configure your SCSI disk controller (controller).
* Configure your graphics card and monitor (x11).