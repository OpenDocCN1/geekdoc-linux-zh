
# 318 Configuring Wireless Networking

| Table 3-1 (continued) |
|---|---|
| IPV6INIT | When set to yes, initializes IPv6 configuration for the wireless interface. Set it to no if you are not using IPv6. |
| MODE | The mode of operation of the wireless network card. Set to Managed for a typical network that connects through a wireless access point. |
| NAME | A nickname for your wireless network. If you don't specify it, the host name is used as the nickname. |
| ONBOOT | Set to yes to activate the wireless interface at boot; otherwise set to no. |
| PEERNDNS | Set to yes to enable the interface to modify your system's `/etc/resol.conf` file to use the DNS servers obtained from the DHCP server (the same server that provides the IP address for the interface). If you set this parameter to no, the file is left unchanged. |
| RATE | Bit rate for connection (set to 1M, 2M, 5M, 11M, or auto). The M means Mbps bits per second. Set to auto to use the maximum possible transmission rate. |
| TYPE | Set to wireless for wireless network interface. |
| USERCTL | Set to yes, a non-root user can control the device. Set it to no so that root can control the device. |

![](img/d9230b719dc0efd80851f363d8c6f571_344_0.png)

Check the status of the wireless network interface, type the following command:

```
iwconfig
```

Here's a typical output from a Fedora Core laptop with a Ethernet PC card:
lo no wireless extensions.
eth0 no wireless extensions.
1 IEEE 802.11-DS ESSID:"HOME" Nickname:localhost.localdomain Access Point: 00:30:AB:06:02:25:E0 Mode:Managed Frequency:2.47GHz Access Bit Rate:19M/s Tx-Power:15 dBm Sensitivity:0 Bit-retry:1 RTS-off Fragr:0 Encryption key:ACEF-00D Power Management:off Link Quality:86/60 Signal level:27 dB Noise level:93 dB Rx Invalid width:0 Rx Invalid crypto:0 Rx Invalid frag:0 Invalid misc:0 Tx excessive retries:0 Missed beacon:0

Here the eth interface refers to the wireless network card. I edited the encryption key and other parameters here, but the sample output shows what you typically see when the wireless link is working.

# Chapter 4: Managing the Network

## In Chapter

- Learning the TCP/IP configuration files
- Checking TCP/IP networks
- Configuring networks at boot time

Like everything else in Fedora Core, TCP/IP setup is a matter of preparing numerous configuration files (text files you can edit with any text editor). Most of these configuration files are in the /etc directory. The Fedora Core installer helps the details of the TCP/IP configuration files. Nevertheless, if you know the names of the files and their purposes, editing the files manually, it is easier.

## Learning the TCP/IP Configuration Files

Running the Network Configuration tool is enough to get TCP/IP configured on your system. However, if you want to effectively manage the network, you need to become familiar with the TCP/IP configuration files you can edit the files, if necessary. (For example, if you want to check whether the name servers are specified correctly, you have to know about the /etc/resol.conf file, which stores the IP addresses of name servers.)

Table 4-1 summarizes the basic TCP/IP configuration files. I describe these configuration in the next sections.

| Table 4-1 | Basic TCP/IP Network Configuration Files |
|---|---|
| This File | Contains the Following |
| /etc/hosts | IP addresses and host names for your local network as well as any other systems you access often |
| /etc/networks | Names and IP addresses of networks |
| /etc/host.conf | Instructions on how to translate host names into IP addresses |
| /etc/resol.conf | IP addresses of name servers |
| /etc/hosts.allow | Instructions on which systems can access Internet services over your system |
| /etc/hosts.deny | Instructions on which systems must be denied access to Internet services on your system |
| /etc/nsswitch.conf | Instructions on how to translate host names into IP addresses |

# 320 Learning the TCP/IP Configuration Files

### /etc/hosts

The /etc/hosts text file contains a list of IP addresses and host names for your local network. In the absence of a name server, any network program on your system uses this file to determine the IP address that corresponds to a host name. Think of /etc/hosts as the local phone directory where you can look up an IP (instead of a phone number) for a local host.

Here is the /etc/hosts file from a system, showing the IP addresses and names of other hosts on a typical LAN:

```
127.0.0.1       localhost       localhost.localdomain
# Other hosts on the LAN
192.168.0.1       1nbp933
192.168.0.50      1nbp600
192.168.0.200    1nbp200
192.168.0.233    1nbp233
192.168.0.40      1nbp400
```

As the example shows, each line in the file starts with an IP address, followed by the host name for that IP address (you can have more than one host name for any given IP).

### /etc/networks

/networks contains the names and IP addresses of networks. These network names are commonly used in the routing command (/sbin/route) to specify a network by name instead of its IP address. Don't be alarmed if your Linux PC does not have the /etc/networks file. Your TCP/IP network works fine without this file. In fact, the Fedora Core installer does create a /networks file.

### /etc/host.conf

Linux uses a special library (that is, a collection of computer code) called the resolver library to obtain the IP address that corresponds to a host name. The /etc/host.conf file specifies how names are resolved (that is how the name gets converted to an IP address). A typical host.conf file might contain the following lines:

```
hosts bind
multi on
```

The entries in the host.conf file tell the resolver library what services to use (and in which order). The option indicates the order of services. The sample entry tells the resolver library to first consult the /etc/hosts file, and then check the nameserver to resolve a name. The multi option indicates whether a host in the /etc/hosts file can have multiple IP addresses. Hosts that have more than one IP address are called multihomed because the presence of multiple addresses implies that the host has several network interfaces (in effect, the host "lives" in several networks simultaneously).

### /etc/resolv.conf

The /etc/resolv.conf is another text file used by the resolver that determines the IP address for a host name. Here is a sample resolv.conf file:

```
search comcast.net
nameserver 192.0.2.1
nameserver 8.8.4.8
```

The first line tells the resolver how to search for a host name. For example, when trying to locate a host, the search directive in the example causes the resolver to try host.comcast.net first, then comcast.net. The nameserver line provides the addresses of name servers for your domain. If you have multiple name servers, they are listed on separate lines. They are queried in the order in which they appear in the file. If you do not have a name server for your network, you can safely ignore this: TCP/IP still works, though you might not be able to refer to hosts by name (other than those listed in the /etc/hosts file).

### /etc/hosts.allow

The /etc/hosts.allow file specifies which hosts are allowed to use the Internet services (such as TELNET and FTP) running on your system. This service is consulted before certain Internet services. The services start only if the entries in the hosts.allow file imply that the requesting host is allowed to use the services. The entries in /etc/hosts.allow are in the form of server:IP address format, where server refers to the name of the program providing a specific Internet service, and IP address identifies the host allowed to use that service. For example, if you want all hosts in your local network (which has the network address 192.168.0.0) to access the Telnet service (provided by the in.telnetd program), add the following line in the /etc/hosts.allow file:

```
in.telnetd:192.168.0.0
```

If you want to let all local hosts have access to all Internet services, you can use the ALL keyword and rewrite the line as follows:

```
ALL:192.168.0.0
```

Finally, to open Internet services to all hosts, you can replace the IP address with ALL, as follows:

```
ALL:ALL
```

You can also use host names in place of IP addresses. To out the detailed syntax of the entries in the /etc/hosts.allow file, type man hosts.allow at the shell prompt in a terminal window.

### /etc/hosts.deny

This file is just the opposite of /etc/hosts.allow — whereas hosts.allow specifies which hosts may access Internet services (such as TELNET and TFTP) on your system, the hosts.deny file identifies the hosts that must be denied services. The /etc/hosts.deny file is consulted if no rules are in the /etc/hosts.allow file that apply to the requesting host. Service is denied if the hosts.deny file has a rule that applies to the hosts.

The entries in the /etc/hosts.deny file have the same format as those in the /etc/hosts.allow file — they are in the form of a server:IP address format, where server refers to the name of the program providing a specific Internet service and IP address identifies the host that must not be allowed to use that service. If you already set up entries in the /etc/hosts.allow file to allow access to specific hosts, you can place the following line in /etc/hosts.deny to deny all other hosts access to any service on your system:

```
ALL:ALL
```

To out the detailed syntax of the entries in the /etc/hosts.deny file, type man hosts.deny at the shell prompt in a terminal window.

# 322 Learning the TCP/IP Configuration Files
