
you want to connect to), and set the encryption key, if any. You can set the option for getting the IP address to DHCP (a protocol for obtaining network configuration parameters, including IP addresses from a server on the network). When you're done and you return to the Network Configuration tool's main window, select the new wireless device and click the Activate button. If all goes well, the wireless network is up and running after a few moments.

![](img/792720823146d68f19fd50c99ebfce4b_319_0.png)

In Fedora Core, the Network Configuration tool saves your wireless network settings in a text file. The name of the text file depends on the wireless network device name. If the wireless network device name is eth0, the configuration is stored in the text file `/etc/sysconfig/network-scripts/ifcfg-eth0`. If the wireless device name is eth1, the file is `/etc/sysconfig/network-scripts/ifcfg-eth1`. This configuration file contains various settings for the wireless network card. Table 3-1 explains the meaning of the settings. Here is a slightly edited version of the `/etc/sysconfig/network-scripts/ifcfg-eth1` file from my laptop PC running Fedora Core:

```text
IPV6INIT=no
USERCTL=no
PEERDNS=yes
TYPE=Wireless
DEVICE=eth1
HWADDR=00:02:2d:8c:f9:c4
BOOTPROTO=dhcp
BOOTBOOT=no
DHCP_HOSTNAME=
NAME=
ESSID='HOME'
CHANNEL=6
MODE=Managed
RATE=auto
```

In Fedora Core, the encryption key is stored separately. For a wireless Ethernet card whose device name is eth1, the encryption key is stored in the `/etc/sysconfig/network-scripts/keys-eth1` file. For example, here is what this file contains for my example:

```text
KEY=1fdf3fdfe
```

![](img/792720823146d68f19fd50c99ebfce4b_320_0.png)

Note that the key has 10 hexadecimal digits for a 40-bit key (for example, `1fdf-3fde-fe`) or 26 hexadecimal digits for a 104-bit key. The keys are, in fact, 64-bit and 128-bit, but the encryption algorithm automatically generates 24 bits of the key, so you need to specify only the remaining bits. Needless to say, the longer the key, the more secure the encryption.

![](img/792720823146d68f19fd50c99ebfce4b_320_1.png)

If you ever manually edit the parameters in the wireless Ethernet configuration file in Fedora Core, type the following command to reactivate the wireless network interface after editing the configuration file:

```text
/etc/init.d/network restart
```

### Table 3-1 Settings in Configuration File for a Wireless Ethernet Network Interface in Fedora Core

| This Parameter | Means the Following |
| :--- | :--- |
| BOOTPROTO | The name of the protocol to use to get the IP address for the interface. It's either dhcp or bootp for an Ethernet interface. |
| CHANNEL | Channel number (between 1 and 14 in United States and Canada). Must be the same as that set for the wireless access point. In managed mode, you don't need to specify the channel. |
| DEVICE | The device name for the wireless Ethernet network interface (eth0 for the first interface, eth1 for the second, and so on). |
| ESSID | Extended Service Set (ESS) Identifier, also known as the wireless network name. It is case-sensitive and must be the same as the name specified for the wireless access point. Provide the name within single quotes (for example, 'HOME'). |
| HWADDR | The hardware address (also called the MAC address) of the wireless network card (six pairs of colon-separated hexadecimal numbers; for example, 00:02:2d:8c:19:c4). The wireless card's device driver automatically detects this address. |
| IPV6INIT | When set to *yes*, this parameter initializes IPv6 configuration for the wireless interface. Set it to *no* if you are not using IPv6. |
| MODE | The mode of operation of the wireless network card. Set to **Managed** for a typical network that connects through a wireless access point. |
| NAME | A nickname for your wireless network. If you don't specify it, the host name is used as the nickname. |
| ONBOOT | Set to *yes* to activate the wireless interface at boot time; otherwise, set to *no*. |
| PEERDNS | Set to *yes* to enable the interface to modify your system's */etc/resolv.conf* file to use the DNS servers obtained from the DHCP server (the same server that provides the IP address for the interface). If you set this parameter to *no*, the */etc/resolv.conf* file is left unchanged. |
| RATE | Bit rate for the wireless connection (set to one of the following options: 1M, 2M, 5.5M, 11M, or *auto*). The M means Mbps or a million bits per second. Set to *auto* to use the maximum possible transmission rate. |
| TYPE | Set to **Wireless** for wireless network interface. |
| USERCTL | When set to *yes*, a non-root user can control the device. Set it to *no* so that only *root* can control the device. |

In SUSE Linux, use YaST to configure the wireless network. SUSE stores the wireless configuration parameters in a file whose name begins with **ifcfg-wlan**, followed by a number such as **0** or **1**, depending on the sequence number of the wireless network interface. The configuration file is stored in the */etc/sysconfig/network* directory. Here is a typical list of wireless configuration parameters from a configuration file in SUSE Linux:

```text
WIRELESS_MODE='Managed'
WIRELESS_ESSID='HOME'
WIRELESS_NICK=''
WIRELESS_RATE='auto'
WIRELESS_AUTH_MODE='open'
WIRELESS_KEY_0='0123-4567-89'
```

![](img/792720823146d68f19fd50c99ebfce4b_321_0.png)

To check the status of the wireless network interface, type the following command:

```text
iwconfig
```

Here’s a typical output from a Fedora Core laptop with a wireless Ethernet PC card. (The output should be similar in other Linux distributions.)

```text
lo        no wireless extensions.

eth0      no wireless extensions.

sit0      no wireless extensions.

eth1      IEEE 802.11b  ESSID:"HOME"  Nickname:"localhost.localdomain"
Mode:Managed  Frequency:2.437 GHz  Access Point: 00:30:AB:06:E2:5D
Bit Rate=1 Mb/s  Sensitivity:1/3
Retry limit:4  RTS thr:off  Fragment thr:off
  Encryption key:1FDF-3FDE-FE  Security mode:open
  Power Management:off
  Link Quality=51/92  Signal level=-40 dBm  Noise level=-91 dBm
  Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:27
  Tx excessive retries:0  Invalid misc:0  Missed beacon:0
```

Here, the eth1 interface refers to the wireless network card. I edited the encryption key and some other parameters to hide those details, but the sample output shows you what you’d typically see when the wireless link is working.

# Chapter 4: Managing the Network

## In This Chapter

- Learning the TCP/IP configuration files
- Checking TCP/IP networks
- Configuring networks at boot time

Like almost everything else in Linux, TCP/IP setup is a matter of preparing numerous configuration files (text files you can edit with any text editor). Most of these configuration files are in the /etc directory. The Linux installer tries to be helpful by hiding the details of the TCP/IP configuration files. Nevertheless, if you know the names of the files and their purposes, editing the files manually, if necessary, is easier.

## Discovering the TCP/IP Configuration Files

You can configure TCP/IP networking when you install Linux. However, if you want to effectively manage the network, you need to become familiar with the TCP/IP configuration files so that you can edit the files, if necessary. (For example, if you want to check whether the name servers are specified correctly, you have to know about the /etc/resolv.conf file, which stores the IP addresses of name servers.)

Table 4-1 summarizes the basic TCP/IP configuration files. I describe these configuration files in the next few sections.

| This File | Contains the Following |
| :--- | :--- |
| /etc/hosts | IP addresses and host names for your local network as well as any other systems that you access often |
| /etc/networks | Names and IP addresses of networks |
| /etc/host.conf | Instructions on how to translate host names into IP addresses |
| /etc/resolv.conf | IP addresses of name servers |
| /etc/hosts.allow | Instructions on which systems can access Internet services on your system |
| /etc/hosts.deny | Instructions on which systems must be denied access to Internet services on your system |
| /etc/nsswitch.conf | Instructions on how to translate host names into IP addresses |
