(anaconda) as described in this chapter. You will be installing Fedora just as you would from a standard install CD/DVD disk like the Fedora spin. The only difference is that only the small subset of applications already on the Fedora Live-CD will be installed. You will not have the option to choose applications during the install process. Given that most applications have to update from the Fedora repository anyway, this is not much of an issue. Just use Add/Remove Software (Pirut) to install the software you want, after you have finished installation. However, if do not have any online access and need certain applications, you would have to use a standard installation CD/DVD spin like Fedora. When you start the Install to Hard Drive process, a window will open, showing the initial install screen, letting you choose to install Fedora. The install process shows fewer screens than the standard process, but performs all necessary tasks. The screens shown are as follows:

+   - **Partitions** Here you set up your partitions. You have the option to use a default set up, or mange your own. See the section on Partition, Raid, and Logical volumes for more information.
- **Network** Specify your network configuration, usually DHCP.
- **Time** Set the time.
- **Password** Enter a password for the root user. This is your administrative password.
- **Format, software install, and post-installation** Your partitions are formatted and all the software from the Live-CD is installed. Then post install procedures are performed like setting up the Grub boot loader.

When you reboot, you will start up the Fedora installation on your hard disk. Initially you will only have the same software available as was on the Live-CD, but you can use Applications | Add/Remove Software to install other applications, like OpenOffice. You may also have to update many of the applications installed from the Live-CD. Click the update notification, which will automatically appear, to start the update process. Applications and updates will be downloaded from the Fedora repository and automatically installed.

# ### Obtaining the CDs and DVDs

The preferred method for obtaining Fedora is to download it from a Fedora mirror site. Red Hat Enterprise Linux, however, is a commercial product whose disks Red Hat will send you. Red Hat Enterprise Linux updates can then be downloaded from the Red Hat Network, now a commercial service.

A detailed description for all the Fedora download options, including all the ISO disks you will need and links to mirror sites, is available at

```text
http://fedoraproject.org/wiki/Distribution/Download
```

Check this site for the latest download procedures.

You can download directly from the Fedora download site at the following link, where you will find directories for the Fedora distributions.

```text
http://download.fedora.redhat.com/pub/fedora/linux/
```