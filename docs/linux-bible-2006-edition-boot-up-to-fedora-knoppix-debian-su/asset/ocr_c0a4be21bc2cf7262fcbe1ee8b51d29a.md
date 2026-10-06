# Chapter 11 ♦ Running KNOPPIX 357

+   ◆ Network card — From the squished penguin, select Network/Internet ❧ Network card configuration to configure your Ethernet card (assuming you don't just want to use DHCP to get your network address).

+   ◆ ISDN — From the squished penguin, select Network/Internet ❧ ISDN to use ISDN to connect to the network.

+   ◆ Wireless Card — From the squished penguin, select Network/Internet ❧ Wavelun to use a wireless Ethernet card to connect to the network. You can instead select ndiswrapper configuration if there is no Linux driver for your card, but you have a Windows driver you can.

In addition to the interfaces available here, you can use the wdialconf command to create your dial-out connection as described in Chapter 5.

# Installing Software in KNOPPIX

Despite the fact that KNOPPIX includes a wide range of software applications, there may be some software package you want to use with that isn't included. For installing while you are running KNOPPIX from the DVD, you can use KPackage.

To start KPackage, click the squished penguin on the KNOPPIX panel and select Utilities ❧ raManage Software in KNOPPIX (kpackage). The KNOPPIX window opens displaying lists of installed and available packages. If there is a package you want to install, type its name into the search box and press Enter. If the package is available, it will be listed, with a notation of whether or not the package is already installed.

If the software package you want to install is available, but not yet installed, select it then click the Install button. KPackage will use the Debian installer to download the package, and all dependent packages, and install them on your computer. Remember that the software being installed in the version of KNOPPIX that is running in RAM. So, the software will disappear the next time you reboot, unless you do something to preserve your data (such as creating a persistent desktop before installing the software you want to).

# Saving Files in KNOPPIX

When you reboot your computer with KNOPPIX, you not only lose KNOPPIX itself but any data and configuration you may have created along the way. That is because, by default, KNOPPIX runs from your system's RAM and non-writable CD DVD. Using tools and procedures that come with KNOPPIX, there are ways in which you can keep that information going forward.

KNOPPIX happily gives you a login name (knoppix) and a home directory (/home/knoppix), each time you boot from KNOPPIX. You can save files to that directory, as well as change your desktop and system configuration information