Before you upgrade you should download and install all of the available patches and updates to the existing Ubuntu version. If your Ubuntu workstation is connected to the Internet, the Update Manager automatically notifies you when a new version of Ubuntu is available, as shown in Figure 3-18.

![](bbox=[0.16, 0.26, 0.88, 0.68])

Figure 3-18: The Ubuntu Update Manager showing a new version available.

Selecting that option automatically downloads the files necessary to perform a complete upgrade to the new version of Ubuntu.

For Ubuntu server versions, you must use the command line software package updater called apt-get (see the section titled "Command Line Package Management" in Chapter 13, "Software Installs and Updates") to obtain the new Ubuntu installation. Just as with the Ubuntu workstation distribution, you can upgrade an Ubuntu server version with the next direct version or the next LTS version.

> Secret
> If you don’t have access to the Internet from your Ubuntu workstation or server, you can upgrade using the alternate install CD but not the LiveCD. When you boot from the alternate install CD it prompts you if the installation is an upgrade of an existing system, and it attempts to maintain your existing documents and settings located in the /home directory structure.