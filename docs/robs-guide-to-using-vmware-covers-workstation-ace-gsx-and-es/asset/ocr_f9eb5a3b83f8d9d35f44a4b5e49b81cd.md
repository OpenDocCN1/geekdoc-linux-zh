# 32 Upgrading GSX Server Software

For both Windows and Linux, it is important to take the following actions if you are going to install a newer version of VMware GSX Server. This is especially important if you are planning to install from an older generation of GSX Server. As an example, if you are running GSX Server version 2.x and are now upgrading to version 3.2:

+   4. Make sure that all virtual machines are in the Power Off state. If your machines are suspended, resume them first, shut down the guest operating system and then power them off. After installing the new GSX Server software, you will need to upgrade the virtual hardware. See the GSX Server Administration Guide if this applies to you. Also check out the information about VMware generations on page 98.
+   5. Save all undoable disk mode information into the virtual disks. When you have disks that are in the legacy undoable mode, make sure that you save all the changes into virtual disks or discard the changes before powering off.

Also, make sure that you create a backup of your virtual machines and your GSX Server Host machine. And last but not least, test the newer version of VMware GSX Server before you install it into your production environment.

Before you can install a newer version of VMware GSX Server on Windows, you must uninstall your current version. For Linux, it depends on the previous installation method. If you have used the tar installer, you do not have to uninstall the previous version. You only need to ensure that no old extracted files from a tar installation exist in the directory where you extract your download. When you use the RPM installer, you must first uninstall the current version before you can install a new one. To find out whether you have installed with the RPM package, use the following command to query the RPM database:

```
rpm -qa | grep VMware
```

If no entry from the database is shown, then you can assume that the installation was done with the installer from the tar archive. If you need to uninstall the application, which was installed with the RPM package, use the following command:

```
rpm -e VMware-gsx
```

The RPM database listing that you performed with the query command shows all the installed software. The keyword VMware-gsx is used to uninstall the GSX Server, but the VMware console could also be shown in this listing.