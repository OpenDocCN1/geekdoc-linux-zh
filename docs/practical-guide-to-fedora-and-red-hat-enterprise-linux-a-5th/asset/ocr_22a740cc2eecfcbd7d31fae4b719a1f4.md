![](bbox=[0.38, 0.09, 0.8, 0.35])

# Figure 3-9 The Software Selection screen

configuration under Enable IPv4 support and enter the IP address and netmask of the system in the appropriate boxes. You can also set up or disable IPv6 networking on this screen. Click OK.

If you are not using DHCP, click the radio button labeled manually under Set the hostname in the network configuration screen and enter the name of the system. When you turn off DHCP configuration in the Network Devices frame, Anaconda allows you to specify a gateway address and one or more DNS (name-server) addresses. You do not have to specify more than one DNS address, although it can be useful to have two in case the first nameserver stops working. Click Next.

# Software Selection

(This screen does not appear when you install from a live CD.) As the Software Selection screen explains, by default Anaconda installs a basic Fedora system, including software that allows you to use the Internet. See Figure 3-9. Near the top of the screen are three check boxes that you can put ticks in to select categories of software to install: Office and Productivity (FEDORA only; selected by default), Software Development, and Web Server.

Fedora/RHEL software is kept in repositories (see Chapter 13). In the middle of the screen are check boxes (FEDORA only) you can put ticks in to select repositories that hold the following items:

+   Installation Repo—Indicates Anaconda is to install from the repository included on the installation medium.

+   Fedora 12 - xxx—Indicates Anaconda is to use the online Fedora 12 repository. The xxx indicates the system architecture (e.g., i386).

+   Fedora 12 - xxx - Updates—Indicates Anaconda is to use the online Fedora 12 Updates repository. The xxx indicates the system architecture (e.g., i386).