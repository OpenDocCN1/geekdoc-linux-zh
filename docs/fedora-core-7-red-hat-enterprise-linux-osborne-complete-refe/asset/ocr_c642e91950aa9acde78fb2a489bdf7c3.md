# iwspy

Your wireless device can check its connection to another wireless device it is receiving data from, reporting the quality, signal strength, and noise level of the transmissions. Your device can maintain a list of addresses for different devices it may receive data from. You use the **iwspy** tool to set or add the addresses that you want checked. You can list either IP addresses or the hardware versions. A + sign will add the address, instead of replacing the entire list:

```
iwspy eth0 +192.168.2.5
```

To display the quality, signal, and noise levels for your connections, you use the **iwspy** command with just the device name:

```
iwspy eth0
```

# iwl list

To obtain more detailed information about your wireless device, such as all the frequencies or channels available, you use the **iwlist** tool. Using the device name with a particular parameter, you can obtain specific information about a device, including the frequency, access points, rate, power features, retry limits, and encryption keys used. You can use **iwlist** to obtain information about faulty connections. The following example will list the frequencies used on the **eth0** wireless device:

```
iwlist eth0 freq
```

# linux-wlan

The linux-wlan project ( [**www.linux-wlan.org**](http://www.linux-wlan.org)) has developed a separate set of wireless drivers designed for Prism-based wireless cards supporting the new 802.11 wireless standard. The linux-wlan drivers are not currently included with Fedora; you will have to download the drivers. The original source code package is available from the linux-wlan site at [**www.linux-wlan.org**](http://www.linux-wlan.org). The current package is linux-wlan-ng. You will have to unpack and compile the drivers as noted for source code software packages in the preceding chapter.

The drivers will install WLAN devices, with device configurations placed in the / **etc/sysconfig/network-scripts** directory. For example, the configuration for the first WLAN device will be in the **ifcfg-wlan0** script. General wireless options are placed in the / **etc/wlan.conf** configuration file.

# Setting Up Your Firewall: system-config-securitylevel

To set up your firewall , run system-config-securitylevel on your system (Security Level in the System Administration window and menu). In version 1.8, you can enable or disable your firewall with the Enable and Disable buttons (see Figure 5-5). You can run your firewall on a stand-alone system directly connected to the Internet, or on a gateway system that connects a local network to the Internet. Most small networks now use dedicated routers for Internet access which have their own firewalls. Version 1.7 of system-config-securitylevel also includes a panel for enabling and disabling SELinux (which can also be done with system-config-selinux. There is no separate panel for other firewall ports.