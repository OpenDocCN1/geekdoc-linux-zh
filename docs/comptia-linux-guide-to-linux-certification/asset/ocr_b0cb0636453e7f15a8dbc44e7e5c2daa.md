the yum groupremove packagegroupname command to remove all of the RPM packages within a particular package group.

The GNOME and KDE desktop environments on Fedora 20 contain a utility that periodically checks for updated RPM packages for the software installed on your system. If you select the Install Updates option in the notification window, this utility notifies you of any newer packages and automatically downloads and installs them using the yum command. You can also run the graphical **Software utility** shown in Figure 11-5 to check for software updates manually, search for and install new RPM software packages, or manage installed RPM software packages. To start the Software utility within the GNOME desktop environment, navigate to Activities, Show Applications, Software.

# Working with the Debian Package Manager (DPM)

The Debian Package Manager (DPM) is used by default on Linux distributions that are based on the Debian Linux distribution, such as Ubuntu Linux. Like RPM packages, DPM packages contain software that has been precompiled for a specific platform, and they may have package dependencies. However, DPM packages use the .deb extension and are installed and maintained by the `dpkg` command. For example, to install the bluefish Web page editor on an Ubuntu Linux system from the downloaded DPM file `bluefish_2.2.6-1_amd64.deb`, you can use the `dpkg -i bluefish_2.2.6-1_amd64.deb` command. Table 11-9 displays a list of common options used with the `dpkg` command.

![](bbox=[0.15, 0.49, 0.84, 0.92])

Figure 11-5 The Software utility