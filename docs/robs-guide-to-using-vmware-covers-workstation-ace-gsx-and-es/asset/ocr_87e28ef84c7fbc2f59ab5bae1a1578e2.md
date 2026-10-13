this feature on the Workspace tab. You can configure this check to be performed daily, weekly (default), or monthly. It does not automatically install the new software, but it does warn you when a newer version is available for downloading. The automatic check can also be disabled by selecting Never in the update configuration.

# 2.3 Upgrading From a Previous Version

For computers with a Windows host operating system, where an existing version of VMware is already installed, the upgrade process has become much easier with version 5. For previous upgrades, the older version had to be deleted and the entire process, including the new installation required at least two reboots. This has been greatly simplified, because the upgrade now removes the current version and installs version 5 without the need to reboot.

For computers with a Linux host, it depends on the installation method that you used for the previous installation. If you used the tar installation method, then there are no extra steps that you need to take. You can start the installation process from the distribution files. The only thing that you must do first is to delete any old tar installation files that may still be in your present working directory. If the directory vmware-distrib exists, delete it first, before extracting the installation archive.

When you use the RPM installer, you must first uninstall the current version before you can install a new one. To find out whether your installation was made with the RPM package, use the following command to query the RPM database:

```
rpm -qa | grep VMware
```

If no entry from the database is shown, then you can assume that the installation was done with the installer from the tar archive. If you need to uninstall the application when it was installed with the RPM package, use the following command:

```
rpm -e VMwareWorkstation
```

The RPM database listing that you performed with the query command shows all the installed software. The keyword VMwareWorkstation is used to uninstall the Workstation. It could also be another keyword from the database, depending on the version you are running.

# Preparing for the upgrade

Before upgrading the software, virtual machines must be prepared.

+   1. Make sure that all virtual machines are in the Power Off state. If your machines are suspended, resume them first, shut down the guest operating system, and then power them off. After installing the new GSX Server software, you will need to upgrade the virtual hardware. See the GSX Server