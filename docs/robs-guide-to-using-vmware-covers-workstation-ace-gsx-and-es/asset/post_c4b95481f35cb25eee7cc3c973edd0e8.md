
into your virtual infrastructure. Other examples are VirtualCenter and vMotion applications which can help you manage your virtual machines and move them from one hardware platform to another, if they are stored on a Storage Area Network.

Last but not least, the server products come with support for your virtual environment. This is possibly the most important feature of the server products if you plan on using VMware technology in your production environment. You will likely have support for your operating systems and your hardware, so it is very important to have a supported virtual infrastructure as well.

## 2 Fast Track to VMware Workstation

This chapter contains everything you need to know when you get started with VMware Workstation. Experienced users may find the new information on upgrading from a previous version interesting. Chapter 3 explains what is new in VMware Workstation version 5 in detail.

In this chapter, I will cover the basics and will make sure that you have the important information that you need to get your virtual machine up and running. All other basic information is covered in the VMware manual; therefore, I will not discuss the basic information, such as how to add a USB device or a printer to your virtual machine in detail. The people at VMware have done an excellent job of explaining the day to day operations in their documentation and in the products’ help files.

## 2.1 Set Up the Hardware and Host OS

VMware Workstation runs on almost any PC that you have available, starting with Pentium II and Celeron versions. A full list of hardware specifications and requirements can be found at VMware’s website at the following url: www.vmware.com/support/ws5/doc. The two most important items that you need when getting started with VMware Workstation are memory and disk space; you need lots of memory and lots of disk space. You can read more about optimization steps that you can take as well as advanced configurations for working with virtual machines in part 2, which covers general configuration and tips. The minimum amount of RAM that you need to start working with VMware and to have acceptable performance is 512 MB. If you run a virtual machine that uses 256 MB, it leaves the other 256 MB for your host operating system. For every virtual machine that you install, you need at least 1.5 GB of disk space.

As a host, you need either Windows or Linux. You will have to decide on one of these before you buy the software, because every operating system requires its own version of VMware Workstation and both require their own license.

### Windows

Simply put, the only Windows versions that are not supported in VMware are Windows 9x and Windows NT. All the other versions can be used ranging from Windows XP Home Edition to Windows Server 2003. If you have a 64 bit system, you can also install a Windows XP or Windows Server 2003 64 bit edition to use the VMware Workstation. The software itself is still 32 bit so you will not gain any benefits. Also, your guest will run in 32 bit legacy mode inside the virtual machine.

![](img/25fe75b93b97a021effaba85db112a52_24_0.png)

Tip: At the time of writing this book the beta version of VMware Workstation version 5.5 supports running 64 bit operating systems as a host and as a guest.

### Linux

The list with supported Linux distributions on VMware’s website is rather long. If you need detailed information about the distribution on which you want to install VMware Workstation, you can check the full listing at the following URL: www.vmware.com/support/pubs. Most current versions of Mandrake, Red Hat and SuSE are supported. Not only the professional workstation and server version, but also the ‘consumer’ editions like Red Hat Linux 9 and SuSE Professional 9.x are supported.

Tip: When installing your Linux host, make sure to select the packages for the C compiler and kernel development. These are not enabled by default. I suggest that you install them because it is very likely that there are kernel modules for VMware or other products that you want to install, which do not match the kernel you are running and will need to be compiled. Installing these packages after your host has already been installed is time consuming and you could run into some inconsistencies. An example of this is when your kernel is updated by an update process and the packages that you install from the CD-ROM are from an older version.

## 2.2 Get the Software

First, you will need to get the software. You can start out with an evaluation version that you can download from: www.vmware.com/download. You can also apply for a 30 day evaluation copy. The software that you download is the same for both the evaluation period and when you buy a license. So you do not have to re-install the VMware Workstation.

At the time of writing this book, September 2005, the most current version is VMware Workstation 5.0, build 13124. This is also the version that is used for all configurations and examples in this book. Many of the tips and configuration options also apply to the VMware server versions.

### Get a discount

VMware Workstation is available for Windows or Linux. You choose the host operating system when you buy your copy. So, if you buy the Windows version and decide to switch to Linux, you will have to buy an additional copy, and vice versa.

The price for each (Windows or Linux) is USD 189.00 for electronic distribution and USD 199.00 for packaged distribution. An upgrade to version 5 from version 4.x costs USD 99.00 (these prices are as of September 2005). You are eligible for a 5% discount if you enter the following discount code when you buy your product on-line at the VMware Store: VMRC-ROBBAS389. This code is valid for VMware Workstation and VMware GSX Server purchases.

Note: Do you have the latest version? VMware includes an auto update feature that checks the availability of new software. Open Edit → Preferences to configure this feature on the Workstation tab. You can configure this check to be performed daily, weekly (default), or monthly. It does not automatically install the new software, but it does warn you when a newer version is available for downloading. The automatic check can also be disabled by selecting Never in the update configuration.

## 2.3 Upgrading From a Previous Version

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

### Preparing for the upgrade

Before upgrading the software, virtual machines must be prepared.

- 1. Make sure that all virtual machines are in the Power Off state. If your machines are suspended, resume them first, shut down the guest operating system, and then power them off. After installing the new GSX Server software, you will need to upgrade the virtual hardware. See the GSX Server
