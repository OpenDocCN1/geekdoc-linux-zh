# Part II: Ubuntu for Desktop Users

# # Configuring broadband Modems and Dial-Up Connections.

Although broadband Internet access is common nowadays, dial-up connections using protocols such as PPP (Point-to-Point Protocol) are still the way in which some people connect to the Internet. Depending on your geographic location, this may be your only option for connecting to the Internet. Unfortunately, many modern modems are so-called Win-modems, which saves hardware costly by using Microsoft Windows device drivers and the operating system itself to do MODulation/Demodulation gives them their name. Unfortunately, such devices are rarely favored for Linux. See http://linmodems.org for information on whether your modem is a Win-modem and if there is software that may be able to work with Linux.

Using a modem to connect to the Web is rare nowadays, and for that, Ubuntu systems don't install packages for modem configuration and setup by default. If you need to use a modem and have one that works on Linux systems, the graphical gnome-ppp and ppp packages can make it easy for you to configure and initiate modem-based connections. Similarly, the wdwial package that is available in the Ubuntu repositories is a great command-line utility to initiate a PPP or SLIP connection over your modem. See the man page for wdwial, its FAQ (http://alumnit.ca/wiki/index.php?page=WdialFAQ), or its home page (http://freshmeat.net/projects/wdwial/index.php) for information on configuring and using this package. If you are reading this, I apologize for not discussing these packages in detail, but I don't have a dial-up account anymore (or enough phone lines to test with the stack of retired modems that are in my basement).

# # Network Testing with Network Tools

To maintain its tradition of easy graphical network tools, Ubuntu provides a convenient tool that simplifies the current configuration of any of your network interfaces. Ubuntu provides GNOME's Network Tools application to give you a graphical display of network configuration information, as well as easy access to a variety of network tools. Select the System -> Network Tools menu item to start the Network Tools application. This displays a dialog like the one shown in Figure 21-11.

By default, the Network Tools application shows information about your system's loopback interface. To see information about a specific interface, click the Network Device dropdown menu and select the Ethernet interface that you're interested in. Figure 21-11 actually shows information about the primary Ethernet interface, eth0, or one of your tests.

786