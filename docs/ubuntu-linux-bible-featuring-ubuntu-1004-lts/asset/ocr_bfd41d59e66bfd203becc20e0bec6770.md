# Chapter 21: Network Configuration and Security

the Web using a query like Ubuntu Network Manager VPN problem to see if there are any known problems with the type of connection that you are trying to establish. You can also skip using the Network Manager and establish your VPN connection manually. The client-side server that your system must run in order to connect to a specific type of VPN was installed along with the Network Manager plug-in for that type of VPN and is usually integrated into the system process. However, connections will not be automatically started if you need to supply a password or other information during the connection process. See the sidebar "Setting Up and Using OpenVPN Manually" for an example of manually creating configuration files and establishing a connection to a remote OpenVPN server.

# Setting Up and Using OpenVPN Manually

If you don't use the Network Manager to set up your VPN connections (aren't using the Network Manager), you will have to install and configure your VPN connections manually. The type of VPN connection that you use depends on the type of VPN software that is running on the remote system through you are establishing your OpenVPN connection. Although many VPN mechanisms are available for Ubuntu (elbox, OpenVPN, VPNC, etc.), OpenVPN is probably the most common of these, so this section focuses on its installation and configuration on your system. Sorry, Cisco facts!

OpenVPN is a free source VPN package that is released by the GPL and is one of the most popular VPN packages used today. OpenVPN uses the OpenSSL library and SSL/TLS (Secure Sockets Layer/Transport Security) for secure, encrypted communications, and uses prepared secret keys, certificates, or username/password combinations for authentication. Beyond its popularity on Linux systems, OpenVPN is also available for operating systems, FreeBSD, Mac OS X, NetBSD, OpenBSD, Solaris, and Microsoft Windows 2000, XP, Vista, and 2008 Server.

Installing OpenVPN on your system can be done manually by installing the openvpn package which provides the Network Manager's support as a requirement for creating and managing OpenVPN connections. As part of installing OpenVPN, it is integrated into your Ubuntu startup process. As part of startup process, OpenVPN will try to automatically initialize any VPN connections for which configuration files are present in the directory /etc/openvpn. these configuration files must have the extension .conf. Each configuration file identifies the OpenVPN parameters that are required to establish a VPN connection to a remote network, including the name and location of any certificate and key that each connection requires. However, any connections requiring a specific password to unlock or verify a private key will fail during the boot process because OpenVPN does not support storing username and password information in configuration files unless it has specially compiled to do so. Storing username and password information is usually not supported because storing this information in clear text in a configuration file is a huge security hole.

The following is a sample OpenVPN configuration file:

```
port 1194
dev tun
remote whereiework.com
```