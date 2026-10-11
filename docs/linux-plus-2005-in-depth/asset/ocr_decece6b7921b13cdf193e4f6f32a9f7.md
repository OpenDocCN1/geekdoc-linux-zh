# Configuring a NIC Interface

Linux computers in a business environment typically connect to the company network via a NIC. At home, more and more people are connecting to the Internet by means of a NIC, using technologies such as Digital Subscriber Line (DSL) and Broadband Cable Networks (BCNs).

If the NIC was detected during installation, Red Hat Fedora Linux automatically configures the appropriate driver module and prompts the user for the TCP/IP configuration required for the business or home network during installation, as seen earlier in Chapter 3, “Linux Installation and Usage.” However, some NICs are not detected upon installation; these NICs are either detected and configured by kudzu after installation or configured manually.

NIC drivers are usually contained within modules that can be inserted into the Linux kernel; you can use their computer manual, the Internet, or other sources of information to find which Linux module underneath the /lib/modules directory to use for a particular NIC. If there is no module for that NIC underneath /lib/modules, you might need to download a module from the Internet. After the module has been identified or downloaded, this module can be inserted into the kernel using the insmod or modprobe commands discussed in the previous chapter. To load this module at boot time, you should edit the /etc/modprobe.conf file.

The /etc/modprobe.conf file also assigns an alias to the module that can be used when referring the module in a configuration command because modules do not have a corresponding file in the /dev directory. The first Ethernet NIC is given the alias eth0, the second Ethernet NIC is given the alias eth1, and so on. Thus, to load the driver module for the first PCI NE2000 NIC, you could place the following line in /etc/modprobe.conf:

```
alias eth0 ne2k-pci
```

Along the same line, to load the driver module for the second NIC of type DEC Tulip, you could place the following line in /etc/modules.conf:

```
alias eth1 tulip
```

After the driver module for the NIC has been loaded into the Linux kernel, you can configure it to use TCP/IP. The ifconfig command can be used to assign a TCP/IP configuration to a NIC as well as view the configuration of all network interfaces in the computer. To assign eth0 the IP address of 3.4.5.6 with a subnet mask of 255.0.0.0 and broadcast address of 3.255.255.255, you can use the following command at a command prompt:

```
ifconfig eth0 3.4.5.6 netmask 255.0.0.0 broadcast 3.255.255.255
```

Alternatively, you can receive TCP/IP configuration from a Dynamic Host Configuration Protocol (DHCP) or Boot Protocol (BOOTP) server on the network. To obtain and configure TCP/IP information from a server on the network for the first Ethernet adapter, you can use the command dhclient eth0 at the command prompt.