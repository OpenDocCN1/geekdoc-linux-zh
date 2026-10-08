
# Part II: Ubuntu for Desktop Users

continued

```
tls-client
ca ca.crt
cert vonhagen.crt
key vonhagen.key
stu-test
tun-mtu 1500
tun-mtu-extra 32
mssfix 1450
pull
comp-lzo
verb 0
```

These remote, ca, cert, and key entries in OpenVPN configuration files will be different for each VPN connection. The remote key identifies the host that is running the OpenVPN server for a connection, the ca key identifies the file containing the root Certificate Authority certificate for the remote site, the cert key identifies the file containing the client's certificate, and the key key identifies the private key for the client. In this example, the latter two are user-specific, but they can also be sitewide connections. User-specific key files are typically owned by the root user and are stored as mode 600 so that they can only be read by the root user.

The key issue is whether an OpenVPN connection can be automatically created at boot time if the private key file requires a password in order to be used. System administrators can create key files that do not require passwords using the --passpass:password option (where password is a password that will be used automatically) when creating a key file using the openvpn utility. Key files can be used to automatically set up "always-on" VPN connections at boot time. VPN connections use a key file that requires a password and for which all files are stored in /etc/openvpn can be initiated at any time by executing the following command from command-line environment:

```
sudo /etc/init.d/openvpn restart
```

This command will temporarily stop all current OpenVPN connections and then attempt to start all OpenVPN connections for which configuration exists in /etc/openvpn, prompting for any passwords that are required. A more elegant way of setting up an individual OpenVPN connection without interrupting any existing connections is to use a command like the following from any-line environment:

```
sudo openvpn --cd /etc/openvpn --daemon --config configfile.conf
```

The --cd option specifies the directory in which any files without pathname (such as those in the previous example) can be found, the daemon option tells the openvpn daemon to detach from the command-line environment from where it started so the daemon can start correctly, and the --config option specifies the name of the configuration file for the OpenVPN connection that you want to start. You will be prompted for the password for the key file identified in the configuration file, and the OpenVPN daemon will create the connection and put itself in the background in daemon mode. You can see, this command also enables you to store user-specific OpenVPN configuration files in any directory by changing the value of the --cd option to the name of that directory.

# Chapter 21: Network Configuration and Security

OpenVPN connections that you started will persist after you log out, so you should terminate any user-specific OpenVPN connections using the ps command to identify the process ID for the OpenVPN server that you started and using the kill command to kill that process, which will also remove any routing tables for OpenVPN connection. If you are only running a single instance of the openvpn process, you can simplify this by using a command like kill -9 'pidof openvpn' to shut it down.

# Configuration Files for Network Interfaces

Tools such as the Network Manager and WiCd (discussed in Chapter 22) are great if you want flexible, dynamically configured Ethernet interfaces on your system. But what if these don't work for you or if (rasp?) your system doesn't go anywhere or only uses one or two configurations? In these cases, you can eliminate the overhead that mechanisms such as the Network Manager and WiCd introduce by falling back to the original network configuration mechanism that was pioneered by the Debian Linux distribution and has therefore been inherited by ifupscripts over Ubuntu systems: text files.

Network interfaces that rarely change can be easily configured by creating entries for them in the file /etc/network/Interfaces, which is the core network configuration file used on Ubuntu systems. This file supports both wired and wireless interfaces, including security configuration for wireless interfaces. In order to configure your network interfaces using this file, you must first make sure that the Network Manager nor WiCd is running when you start your system. To remove either of these network configuration mechanisms from your system's startup sequence, you must remove the symbolic links S28networkManager and S20wcd from the directory /etc/rc2.d, which is the directory that contains the files from an Ubuntu system up to its default run level, level 2. You can simply remove these links, but I typically like to remember what I did and therefore, create a directory called /etc/rc2.d/DISABLED and move whichever of these symbolic links is present on my system into that directory. This will prevent network configuration mechanisms from running the next time you start your system.

Once you've disabled automatic network configuration mechanisms for your next reboot, you can create entries for your network interfaces in the file /etc/network/interfaces using your favorite editor text. This file will already contain an entry for the loopback interface on your system. The easiest type of entry in this file is an entry for an Ethernet interface that uses DHCP to obtain its IP address and other network configuration information. An entry that defines the Ethernet interface eth0 as one uses DHCP will look like the following:

```
auto eth0
iface eth0 inet dhcp
```

The auto line in this entry states that the interface eth0 will be automatically enabled when the system starts. The iface line in this entry identifies the beginning of the interface definition for eth0, which is a TCP/IP (inet) device that uses dhcp to obtain its configuration information.

# Part II: Ubuntu for Desktop Users

Entries that assign static IP addresses to specific interfaces are equally simple. For example, an entry that assigns a static IP address for the Ethernet interface eth0 will look like the following:

```
eth0
iface eth0 inet static
  address 192.168.6.64
  netmask 255.255.255.0
  gateway 192.168.6.1
```

The auto line in this entry states that the interface eth0 will be automatically enabled when the system starts. The if line in this entry identifies the beginning of the interface definition for eth0, which is a TCP/IP (inet) device with static configuration. The next three lines define the IP address, netmask, and gateway for that interface.

# Manual DNS Configuration

If your network use static IP addresses, your system will not obtain general network configuration information such as DNS server addresses from a DHCP server. You should, therefore, manually create and populate the /etc/resolv.conf file that your system uses to identify its name servers. A /etc/resolv.conf file that uses open DNS servers from OpenDNS is the following:

- domain vonhagen.org
nameserver 208.67.222.222
nameserver 208.67.220.220

The first line in this file identifies the default domain that your system should search for hosts that are specified without domain names. (You will probably use a default domain that is something other than my home domain). You should add entries for any DNS servers that are provided by that default domain, which should appear before entries for the DNS servers from OpenDNS. When your system tries to find the IP address associated with a specific host, it will query the DNS servers in the order in which they are listed in this file.

Information about other DNS servers that are available to the general public, see www.dnsserverlist.org.

Wireless Ethernet interfaces are similarly easy to define in your /etc/network/interfaces file. For example, an entry that defines the Ethernet interface eth1 as one that uses DHCP and the wireless network with the ESSID wwh will look like the following:

```
auto eth1
iface eth1 inet dhcp
  wireless-essid wwh
```
