# 406 Part III ♦ Choosing and Installing a Linux Distribution

# Getting Slackware

Slackware comes on four CDs: two installation CDs and two source code CDs. The first Slackware CD can be used for a good, basic install. If you want to add a full KDE desktop, you need the second installation CD as well. Both are available on the DVD that comes with this.

The full Slackware distribution set is also available from a few dozen mirror sites on the Web (see www.slackware.com/getslack). Because of disk space issues and to maximize bandwidth, the Slackware project recommends you get CD images (ISOs) using BitTorrent. For a list of available torrents, see www.slackware.com/getslack/torrents.php.

> For many years, Slackware was available on one install CD, but adding KDE to the distribution made a second CD necessary.

To support the project, you can purchase the boxed set of Slackware from http://store.slackware.com. At the store, you can also get a subscription to Slackware so that the Slack Store sends you a new version each time one is released (every six to eight months). The store will ship when it's available and charge your credit card. People who like Slackware often pay the subscription to show their support.

# New Features in Slackware 10.2

There are a few significant changes to Slackware 10.2 over previous releases. 10.2, Slackware finally made the leap to support the Linux 2.6 kernel, although it is still in testing mode and you can switch between a 2.6 and 2.4 kernel if you like. Using the newer kernel makes the addition of key features possible:

+   * POSIX Thread Library (NPTL) — Including NPTL can mean tremendous performance improvements for high-demand servers. Although NPTL has been added to 2.4 kernels in some distributions, Slackware is only offering NPTL support for 2.6 kernels.

+   * Hard disk support—SCSI, RAID, and SATA disk support are offered as options for the installer using the test26.s kernel.

+   * Dynamic device creation (Udev) — The Udev feature in the 2.6 kernel allows devices to be created dynamically. This is an important feature for automatic support of devices, such as USB and FireWire, that are plugged in after the system is running, without simply adding every conceivable device name to the /dev directory.