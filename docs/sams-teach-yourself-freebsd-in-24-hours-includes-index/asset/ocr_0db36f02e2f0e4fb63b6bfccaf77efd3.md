# Configuring Network Settings with sysinstall

The simplest way to configure your Ethernet card, and probably the most familiar looking to anyone who's gone through this process on a Windows machine or Macintosh, is with sysinstall. The first time you ask sysinstall to do anything that requires a network connection (a net installation of the system, browsing packages, or various other tasks), it will bring up the network configuration window in which you can set the TCP/IP options for your Ethernet card visually.

An easy way to get to this screen—if you're already up and running multiuser and not in the initial system installation process—is to run /stand/sysinstall, select Configure from the main menu, and scroll down to the Media option. In this submenu, select FTP and some FTP server (it doesn't matter which), and you'll see a dialog box that says Running Multiuser, Assume that the Network Is Already Configured? Choose No to enter the network configuration screens. The next thing that appears is the Network Interface selection screen, shown in Figure 13.2.

Figure 13.2
Selecting your network interface card in the sysinstall program.

![](bbox=[0.32, 0.6, 0.66, 0.8])

You're presented with a list of the interfaces that FreeBSD has found in your system. You'll probably see a number of choices that don't make a lot of sense—aside from choices such as lp0 (the parallel port) and various PPP or SLIP options on your serial ports, you'll see things like gif0 and faith0. These are IPv6 devices; you can ignore them. The option you want is probably at the top. The one we're using in this example is fxp1, an Intel EtherExpress Pro/100B PCI card.

When you select your Ethernet card, you're given two dialog boxes: a choice to let the system try to configure the card automatically using IPv6 and then another choice to let it try using DHCP. Say No to both choices. You'll then be presented with the visual Network Configuration screen, as shown in Figure 13.3.