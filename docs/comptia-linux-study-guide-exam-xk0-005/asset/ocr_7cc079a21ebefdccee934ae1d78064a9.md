```
DEVICE=enp0s3
BOOT=yes
IPV6_PRIVACY=no
```

This configuration indicates that the workstation is using the DHCP process to automatically retrieve network information from a network server. For static IP addresses, you can set the IP address, default gateway, and subnet mask in the configuration file.

Most Linux distributions use the /etc/hostname file to store the local hostname of the system; however, some use /etc/HOSTNAME instead. You will also need to define a DNS server so that the system can use DNS hostnames. Fortunately, this is a standard that all Linux systems follow and is handled in the /etc/resolv.conf configuration file:

```
domain mydomain.com
search mytest.com
nameserver  192.168.1.1
```

The domain entry defines the domain name assigned to the network. By default the system will append this domain name to any hostnames you specify. The search entry defines any additional domains used to search for hostnames. The nameserver entry is where you specify the DNS server assigned to your network. Some networks can have more than one DNS server; just add multiple nameserver entries in the file.

![](bbox=[0.15, 0.495, 0.23, 0.54])

For systems using the systemd startup method, you can use the hostnamectl command to view or change the hostname information. Also, to help speed up connections to commonly used hosts, you can manually enter their hostnames and IP addresses into the /etc/hosts file on your Linux system. The /etc/nsswitch.conf file defines whether the Linux system checks this file before or after using DNS to look up the hostname.

# Graphical Tools

The Network Manager tool is a popular program used by many Linux distributions to provide a graphical interface for defining network connections. The Network Manager tool starts automatically at boot time and appears in the system tray area of the desktop as an icon.

If your system detects a wired network connection, the icon appears as a mini-network with blocks connected together. If your system detects a wireless network connection, the icon appears as an empty radio signal. When you click the icon, you’ll see a list of the available wireless networks detected by the network card (as shown in Figure 7.1).

Click your access point to select it from the list. If your access point is encrypted, you’ll be prompted to enter the password to gain access to the network.