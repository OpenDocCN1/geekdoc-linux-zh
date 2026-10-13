
Administration Guide if this applies to you. Also check the explanation about VMware generations on page 98.

- 2. Save all the undoable disk mode information into the virtual disks. When you have disks that are in the legacy undoable mode, make sure to save all the changes into the virtual disks or discard the changes when powering off.
- 3. Remove any current snapshots that the virtual machines have.

After taking these preparatory steps, the software can be installed on your computer. The individual virtual machines still need to be upgraded.

## Upgrading from a version released prior to version 4

If you are working with a very old version, then additional steps are necessary. For version 2, you need to upgrade the virtual machines to version 3 or 4. Afterwards, they can be upgraded to version 5. VMware version 3 machines need to be upgraded to version 5 before they can be used with version 5.

## Upgrading from version 4

Virtual machines that have been created with version 4 of Workstation can run directly with version 5. There will be some limitations because the new features of version 5, such as using multiple snapshots, are not available. Also, the performance benefits that version 5 offers are not available, if you do not upgrade your virtual machines. If you choose not to upgrade the machine, do not forget to install the newer version of the tools inside the guest operating system. That is the minimum action that you must take after upgrading your host to version 5.

![](img/25fe75b93b97a021effaba85db112a52_27_0.png)

Figure 2.1: This message will warn you if your machine is not already upgraded to a version 5 virtual machine.

As you can see, it is best to upgrade your entire virtual machine to version 5. This is an irreversible operation so make sure to create a backup of your virtual machine first. Upgrading the virtual machine must be done while it is in a power off state. When the machine is powered off, select the Upgrade Virtual Hardware from the VM menu.

After the upgrade has been performed, install the new version of the tools inside the virtual machine. Depending on the version of VMware Workstation that you were running and the operating system inside the machine, additional steps may be necessary for your specific guest. For example, in a Windows 9x machine the display driver needs to be upgraded after upgrading the virtual hardware.

## 2.4 Install VMware Workstation for Windows

The installation of VMware Workstation for Windows is very straightforward. When accepting the license agreement, you will get the usual questions, such as where you would like to place your software. One of the specific questions that will be asked may need some clarification. This question is displayed in Figure 2.2.

![](img/25fe75b93b97a021effaba85db112a52_28_0.png)

Figure 2.2: Prevent unwanted behavior and disable Autorun during installation.

If you leave the CD-ROM autorun enabled, and you run operating systems in your virtual machines which also auto mount CD-ROMs, you will end up with multiple PCs accessing the same CD-ROM. This is not a desirable situation. It will cause strange behavior and will slow down both the host and the guest. Therefore, leave the default setting to disable autorun.

The final step for finishing your installation is to add your VMware Workstation for Windows license. In VMware Workstation, select Help → Enter Serial Number to add the license.

Once the installation has been completed, you can create your first virtual machine. Before you do so, make sure that you understand what types of disks and networking you can choose. Continue with section 2.6 to read more about disk types and networking options.

## 2.5 Install VMware Workstation for Linux

At this point, I am assuming that you have downloaded the installation files, copied them to your computer, or mounted the CD-ROM that contains the installation files. VMware Workstation for Linux is available in two formats: tar archive and an RPM package. I will explain how to install the VMware Workstation for both types of installation files.

Follow these steps to install the software:

- 1. Log on to your Linux host and open a terminal window.
- 2. You need to install the software as a root user so use the su - command to become root.
- 3. For the RPM version, there are two installation methods. One method is to execute the following command to install the software:

```
rpm -Uhv VMware-gsx-3.2.0-14497.i386.rpm
```

Another method to install the RPM package is to click on the file in a file manager in the GUI. Figure 2.3 shows an example of a SuSE 9.3 host, where the RPM is selected in Konqueror. The description of the package is displayed to show what software will be installed. Click on Install package with YaST to install the package. Package managers on other Linux distributions may look different from this, but the installation is just as simple.

![](img/25fe75b93b97a021effaba85db112a52_29_0.png)

Figure 2.3: The RPM package can also be installed from the GUI.

- 4. For the tar archive version, execute the following commands to install the software. First, make the /tmp directory your present working directory or choose another directory where you want to extract the files. This eliminates the need to copy the archive to your hard disk first.

```
cd /tmp
```

Extract the archive with the following command:

```
tar -zxf <path>/VMware-workstation-5.0.0-13124.tar.gz
```

Change the present working directory to the location of the installation files:

```
cd vmware-gsx-distrib
```

Start the installation script:

```
./vmware-install.pl
```

- 5. After the package is installed or when the installation script from the tar archive has completed running, start the VMware Workstation configuration script with the following command:

```
vmware-config.pl
```

- 6. The first action that you have to take is to read and accept the end user license agreement. Read through it and when you are finished, press q to exit the reader. Then type yes, if you agree with the EULA.
- 7. The configuration script will ask you several questions that you need to answer. Here are the default directories that you will be prompted for as well as the default paths that are suggested by the VMware configuration script. They originate from an installation on a SuSE 9.3 professional host. The paths can be different on other Linux distributions.

| Item | Path |
|---|---|
| mime type icons | /usr/share/icons |
| desktop menu entry files | /usr/share/applications |
| application icon | /usr/share/pixmaps |

- 8. At this point in the configuration process, it will try to find a suitable vmmon module for the kernel you are running. If it finds one, the following message will be displayed and the configuration will continue:

The module loads perfectly in the running kernel.

When the pre-compiled modules for your kernel are not available, the following message will be displayed:

None of the pre-built vmmon modules for VMware Workstation is suitable for your running kernel. Do you want this program to build the vmmon module for your system (you need to have C compiler installed on your system)?

At this time you need to have a C compiler and the kernel source files installed. If you have not installed these during the initial Linux installation, you can do that now.

![](img/25fe75b93b97a021effaba85db112a52_31_0.png)

Tip: Be aware that if you install the kernel source from your installation CD-ROM, that version may be different from the one that you are already running. This is because the current one may have been updated by an automated update process. In that case, go through the same update process to update the added kernel development package including the kernel sources.

When a C compiler and kernel source files are available, you will be prompted with the following question:

What is the location of the C header files that match your running kernel?

The default location is: /usr/src/Linux/include.

When it was necessary to build the vmmon module it might show messages saying: Module.symvers is missing' modules will have no modversions and Unable to build the vmmon module.

If that is the case, run the following commands from the Linux source directory, but make that directory the present working directory first:

```
cd /usr/src/Linux
make cloneconfig
make modules_prepare
```

After running these commands, execute the vmware-config.pl configuration script again. Whether the modules will now compile, really depends on your distribution. However, in most cases they will compile. When it does not work after this step, I suggest that you search the VMware knowledge base and the VMware Community Forums for information on your specific installation.
