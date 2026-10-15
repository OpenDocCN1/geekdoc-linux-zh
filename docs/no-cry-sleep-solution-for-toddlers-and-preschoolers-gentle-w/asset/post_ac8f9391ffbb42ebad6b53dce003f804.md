
hostname, and miscellaneous settings. If you use DHCP to automatically configure your network connection, as most networks do, you will most likely not need to do anything on this screen.

The Network devices segment will list your network connection devices, such as your Ethernet device. For computers already connected to a network with an Ethernet card, the first entry is usually labeled eth0. If you need to manually configure your device, entering an IP address for it, you can click Edit to display the device’s configuration panel. Here you can choose to either manually configure the device or use DHCP to automatically configure it. For manual configuration, you can enter the device’s IP address (usually your computer’s IP address) and your network’s netmask.

In the Hostname segment, you can choose either to manually provide your network information or use DHCP to automatically obtain it. If you choose to manually provide your network information, you can enter a hostname and, in the Miscellaneous segment, enter your network’s gateway and DNS servers’ IP addresses.

Following network configuration, the Firewall Configuration screen then lets you create basic default levels of network security. You can opt to use default firewall rules or customize your configurations, specifying trusted devices and services to allow such as Web or FTP connections. The firewall configuration still implements the newer IP tables firewall rules (see Chapter 19).

## System Configuration

The next screen lets you choose the language you want to use.

On the Time Zone Configuration screen, you have the option of setting the time by using a map to specify your location or by using Universal Coordinated Time (UTC) entries.

On the next screen, you can set the root password for the root account on your system. This is the account used for system administration operations, such as installing software and managing users. After installation, a similar screen will let you also add ordinary user accounts.

## Software Installation

You can then select the packages you want to install on your system. Red Hat lets you choose a set of predetermined collections tailored to personal desktops, workstations, or servers. You can select one of these package configurations or choose a custom installation. On the custom installation, you can select groups of packages, such as those for GNOME, KDE, different servers such as Web or FTP servers, games, editors, and development support, which includes compilers and debuggers. To install all packages, select the Everything entry at the end of the list.

## X Window System Configuration (Red Hat only)

considered essential to the category described. In the Web Server category, the standard segment contains the Apache Web server, and the Extra segment contains added modules and servers such as Squid and Tux.

The packages are then installed, showing each package as it is installed and the progress of the installation. (For the Red Hat DVD-ROM included with this book, the DVD-ROM will install in one continuous operation. The install program detects all packages as residing on the single DVD-ROM. There are no ejecting or inserting tasks as there are with CD-ROMs.) If you are using CD-ROMs instead (purchased from Red Hat or downloaded from the Internet), you will be prompted when to install the next CD-ROM. The current one will automatically be ejected for you. When the installation finishes, a postinstall process will complete. You are then usually given the option to create a boot disk. You can use this disk to access your Linux system should your hard disk boot somehow fail.

For Red Hat, X configuration then completes the installation. (Fedora automatically detects your graphics card before installation.) This enables GUI interfaces, such as GNOME and KDE. X configuration uses the redhat-config-xfree86 utility to detect your video card and monitor automatically.

You first have to select and choose your video card on the Graphic Interface screen. redhat-config-xfree86 will initially probe your card and select it from a list of video cards shown on the screen, along with the amount of memory on the card. Check to see if your card is selected. If not, locate your card in the list and click it. You will need to know the brand and model number for your card. If your video card does not appear on the list, you can try specifying just the chipset. Find out the chipset used on your card and select it in the Generic Video Card entry. This entry will list several commonly supported chipsets. If your card or chipset is not present, you should skip the X configuration process. Just click the Skip X Configuration check box. You can later try to use X configuration utilities such as redhat-config-xfree86 or try to configure the /etc/X11/XF86Config configuration file directly. This requires technical expertise.

If you know how much video memory is on your video card, you can check for the appropriate entry for that amount located in the drop-down menu. If an incorrect amount is selected, you can select the appropriate one.

On the Monitor Configuration screen, you select your monitor. Initially, redhat-config-xfree86 will automatically probe your monitor and select a make and model from those listed on the screen. Check to see that the correct monitor is selected. If not, find its entry and click it. Monitor entries are organized by company in an expanding tree. For example, if you have a Hewlett-Packard monitor, click the triangle symbol next to the Hewlett-Packard entry to list all the monitors that Hewlett-Packard makes. Then click your model. When you select a monitor, the horizontal and vertical boxes at the bottom of the screen will display your monitor’s horizontal sync range and vertical sync range (these values are generally available in the documentation that accompanies your monitor or from your monitor’s vendor or manufacturer).

If your monitor does not appear on the list, select a Generic (usually Generic multisync) or Unprobed entry. redhat-config-xfree86 will then supply horizontal and vertical frequency values in the labeled boxes at the bottom of the screen. Check that the correct horizontal and
