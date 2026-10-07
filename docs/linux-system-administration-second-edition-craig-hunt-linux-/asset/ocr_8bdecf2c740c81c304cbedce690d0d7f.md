# Configuring Networking

If your system has a network card, Red Hat Linux asks you to specify your network configuration, as shown in Figure 2.4. Enter the necessary information manually, or click the Configure Using DHCP button if your network uses a DHCP server to dish out IP addresses. Chapter 12 describes the TCP/IP networking options in more detail, if you need to set these options manually and don't know what to enter. (In this case, you'll need to consult with your network administrator to learn what to enter.)

![](bbox=[0.12, 0.195, 0.85, 0.57])

Figure 2.4: If you enter TCP/IP networking information during installation, you won't have to do so again after installation.

# Configuring the Firewall

Following the Network Configuration screen, you'll see the Firewall Configuration screen. Your choices are High Security, Medium Security, and No Firewall. You may also customize the firewall rules. The default settings of a High Security firewall set up a system that will only accept DHCP connections, DNS replies, and connections that you have specifically defined. While this is the most secure, it is not practical on a system that runs a lot of services like FTP or IRC since those services would deny any connection from a site that has not been specifically allowed through. You may also set up a Medium Security firewall that allows you to define type of connections to allow through. You might also choose to trust any packets from a given interface. We'll discuss these concepts thoroughly in Chapter 15, "Security."

# Configuring the Time Zone

After a self-explanatory Language Support Selection screen, the installer starts the Time Zone Selection screen. There are so many time zone options as to make this a bigger task than it sounds. Select the appropriate zone for your location or the offset from Universal Coordinated Time (UTC). In either case, you must specify whether your system clock uses UTC. If you use the offset method, you must also specify whether or not Daylight Savings Time is needed.