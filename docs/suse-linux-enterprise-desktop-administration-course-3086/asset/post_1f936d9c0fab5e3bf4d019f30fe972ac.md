
**GConf** The system software used to configure GNOME preferences.
**gconf** The GConf daemon.
**gconf-editor command** A command that is used to invoke the graphical GConf editor.
**gconftool-2 command** A command that is used to invoke the terminal-based GConf editor.
**GNOME Control Center** A graphical utility that can be used to configure the behavior of the GNOME desktop environment.
**GNOME Volume Manager** A software system that mounts and manages access to removable media devices such as CD-ROMs, DVDs, and USB devices.
**gnome-volume-manager command** A command that is used to invoke the GNOME Volume Manager.
**gnome-Xgl-settings command** A command that is used to start the Desktop Effects tool within a GNOME desktop environment.
**Keys** Configuration parameters that contain values used by GConf.
**kwin** The default window manager in the KDE desktop environment.
**lsmod command** A command that lists currently loaded kernel modules.
**Metacity** The default window manager in the GNOME desktop environment.
**OpenGL** An industry standard application programming interface for defining 2D and 3D graphical images.
**OpenOffice.org** A full-featured office productivity suite commonly used on Linux systems today.
**sabayon** The package name for the Desktop Profile Editor.
**sax2 command** A command that is used to start the X configuration utility on a SUSE Linux system.
**template** A sample structure used to create new documents within a program such as OpenOffice.org.
**udev** A Linux software system used to create and manage device files for system devices.
**window manager** A software component that controls the look and feel of applications and dialog windows in X.
**X** The system used to draw graphical images on a Linux system.
**Xgl** An OpenGL-based software architecture that can be used with X.
**xnest** An X server that displays its output within a window in an existing X session.

## Review Questions

+   1. If you activate the Compiz window manager in a GNOME desktop environment, which window manager will it replace?
+      a. kwin
+      b. kde
+      c. Metacity
+      d. Enlightenment
+   2. What command can you use to configure X settings such as video card and monitor type from a command prompt if you do not currently have an X server running? ________

3. What key combination can be used to unfold the Compiz cube?
a. Ctrl+Alt+Left
b. Ctrl+Alt+Shift+Left
c. Pause
d. Ctrl+Alt+Down

4. You have used the GConf editor to modify your GNOME desktop settings for Nautilus. You know that these settings are stored in a %gconf.xml file. Which directory should you examine to locate the file that contains your Nautilus settings?
a. /opt/gnome/nautilus
b. ~/.gconf/apps/nautilus
c. ~/.gconf/nautilus
d. /opt/gconf/nautilus

5. What commands can be used to edit GConf configuration files? (Choose all that apply.)
a. gconf-editor
b. gconf-config
c. gconftool-2
d. vim

6. You are trying to change the systemwide GNOME defaults with gconftool-2, but you are unable to do so. What must you do? __________

7. GConf can be used to lock down a GNOME desktop such that users are unable to modify certain desktop settings. What can you configure to lock down desktop settings? (Choose all that apply.)
a. Set mandatory preference values in the GConf editor.
b. Create user profiles.
c. Select Edit > Lockdown in the Desktop Profile Editor.
d. Select Desktop > GNOME > Lockdown in the GConf editor.

8. You have created a profile for a specific user using the Desktop Profile Editor and would like to verify its location on the file system. What file contains the user’s desktop profile? __________

9. You have created a custom configuration file for Firefox that you would like given to new users that will be created on the system. What should you do? __________

10. Which of the following methods for restricting user access to removable media is the most effective?
a. Using GConf to prevent the automounter from mounting removable media
b. Adding “noauto” to the /etc/fstab file

+   c. Preventing the usb_storage kernel module from loading at system initialization
+    d. Physically removing or restricting access to CD-ROM drives, DVD-ROM drives, and USB ports

## Discovery Exercises

![](img/9129877170834ca9d5fdac5319bf5f12_597_0.png)

### Creating a Lockdown Security Profile

Security planning is vital when planning to lock down computers within your organization. Effective security planning ensures that security loopholes are detected in a flawed design before they are implemented.

You are about to implement several new publicly accessible kiosks for individuals who want to browse your company catalog. This catalog is made available on the Internet and will be accessed using Firefox from the kiosks. Kiosk users should be restricted to using the Firefox application only and should not have any access to other areas of the desktop or removable media. In addition, they should not be able to customize Firefox or change its default home page. The administrator user account should have full access to the system to perform system maintenance.

Write a short summary of the steps needed to perform this lockdown. Include the names of the technologies and tools involved and how they can be used to lock down the kiosks. If there are multiple methods that can be used to lock down a particular area, provide a rationale for the method you chose.

### Locking Down Computers

Assume that your PC is a publicly accessed kiosk and configure GConf to lock it down using the summary you created in the previous Discovery Exercise. Test your results to ensure that the lockdown is effective.

### Researching Lockdown Utilities

Locking down Linux computers has been a standard practice for over a decade. As a result, there are many software packages in addition to GConf that can be used to restrict access to various Linux components or lock down the entire Linux desktop. Use the Internet to research three lockdown packages. For each, describe their function and basic configuration. Next, compare each lockdown package to GConf. Summarize your findings in a brief memo.

## Deploy SUSE Linux Enterprise Desktop 10

This section explains how to deploy SUSE Linux Enterprise Desktop 10. Which deployment method you choose will depend to a large degree on the number of workstations you want to deploy. The installation of hundreds of machines requires a different approach than the installation of just a few.

## Objectives

+   - Objective 1—Installation Options and Deployment Strategies
+   - Objective 2—Autoinstallation Basics
+   - Objective 3—The Configuration File for AutoYaST
+   - Objective 4—Installation Server: Setup and Use
+   - Objective 5—Automated Installation

## Objective 1—Installation Options and Deployment Strategies

If you are installing a single machine, a manual installation using the installation DVD is the best option. However, alternatives are needed when the number of machines you plan to install increases.

You can start the installation using the *SUSE Linux Enterprise Desktop 10* DVD, a boot disk, or a PXE-capable network card. The installation source can be the DVD or an installation server in the network. The supported protocols for accessing the repository on the installation server are NFS, HTTP, FTP, and SMB/CIFS.

To find the optimum solution for your network, you need to understand the following:

+   - Installation Options
+   - Deployment Strategies

### Installation Options

Before you decide which method you will use to install *SUSE Linux Enterprise Desktop 10*, you need to consider the following:

+   - Boot Media
+   - Installation Source
+   - Configuration

### Boot Media

To install a machine, you have to choose a boot medium to boot the machine:

+   - *Installation DVD*—The installation DVD is bootable and can be used to start the installation or to boot a rescue system. Different kernel parameters can be set if you have trouble with the default parameters. For example, it is possible to disable ACPI or local APIC, or to use safe settings.
+   - *Floppy disk*—To create bootable floppy disks, start YaST and select System > Boot or Rescue Floppy.
+   - *PXE-capable network card*—If the machine is equipped with a PXE-capable network card, it can load the boot image from a TFTP server in the network. If the network card also supports Wake on LAN, a completely remote installation is possible.

### Installation Source

You can use different installation sources:

+   - Installation DVD
     The installation DVD contains all files needed to install *SUSE Linux Enterprise Desktop 10*.
+   - Installation Server
     The files needed for installation can be stored on a server in the network. Protocols available are HTTP, FTP, NFS, or SMB/CIFS. SLP can be used to advertise the installation server in the network.
