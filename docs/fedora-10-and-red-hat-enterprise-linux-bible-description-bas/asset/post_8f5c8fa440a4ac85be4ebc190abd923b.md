
# Chapter 15: Setting Up Network Connections and LANs 677

The freq q parameter displays the available frequencies (and channels) available for communication. Note that all the available frequencies are in the 2.4 GHz range.

```
# iwlist eth0 rate
eth0 6 available bit-rates :
1Mb/s
2Mb/s
5.5Mb/s
11Mb/s
58Mb/s
39.5Mb/s
Current Bit Rate=54Mb/s
```

The preceding rate parameter displays the transmission rates available for the wireless interface. If you don't, 1, 2, 5.5, and 11 Mbps are available for the current interface.

```
# iwlist eth0 key
eth0 2 key sizes : 40, 104bits
4 keys available :
[1] 7365-6375-31 (40 bits)
[2] off
[3] off
[4] off
Current Transmit Key: [1]
```

The key parameter lets you see the encryption keys available with the interface. It also shows the key sizes currently available. Because the card reflected in the preceding example supports 64- and 128-bit encryption, the key sizes available are 40 and 104 bits. (The encryption algorithm automatically generates the last 24 bits of each key.)

If you are troubleshooting your wireless LAN connection, some settings are more likely than others to cause problems. It is important to set the following wireless LAN settings properly — if you don't, they may keep your network from working:

- Network ID (ESSID) — You may not be able to communicate among peer computers if the Network ID (ESSID) doesn't match on each of them. Network IDs are case sensitive — for example, Mylan is not the same as MyLAN.
- Encryption key — Having encryption keys that aren't like trying to log in Linux with the wrong password. Check that all nodes are using the same key. If you were unable to connect, check the encryption key first, because typing hexadecimal keys can be to error.
- Mode — If you are communicating through an access point, your mode should be set to Managed and you must provide the MAC address for that access point. In many single-cell networks, you should set all nodes to Ad hoc. The Ad hoc mode allows all nodes to communicate directly to each other as peers.

# Part IV: Fedora RHEL Network and Server Setup

- Channel or frequency — The channel and frequency options are just two different means of setting the same value. For example, setting the channel to 1 is the same as setting the frequency to 2.412G (GHz). Make sure the nodes on your network are able to communicate on the samefrequency.

## Checking TCP/IP

To ensure your wireless LAN is communicating with its peers, use the `ping` command as described earlier in this chapter. If you believe that your cards are working properly, but the ping command continues to give you a Network Unreachable message, you may have a problem with your TCP/IP configuration. Here are some items you can check from the Network Configuration window:

- IP address — Know the IP address of the peer you are trying to reach.
- Hostname — If you ping the computer by name, make sure your computer can properly resolve that name into the IP address, or the peer's hostname and IP address properly listed in the /etc/hosts file. The former option will probably require that you have one or more DNS servers identified to resolve the name.

If you can reach another computer on the wireless LAN, but not computers outside of that LAN (such as Internet addresses), check that you have properly identified the location of your gateway. If the gateway address is correct, and you can reach that gateway, it may be that the gateway itself is not configured to allow packet forwarding.

If you found that any of the preceding information needed to be changed and you changed it, you should restart the LAN interface. One way to do that is to restart the PCIA interface and the network interfaces as follows:

```
# /etc/init.d/pcmcia restart
# /etc/init.d/network start
```

## Adapting to poor reception

Your wireless LAN may working fine while your wireless computers are sitting on the same desk. If performance degrades when you separate the computers, you may need to identify any obstructions. Then you must decide how to get around them. For desktop systems, a small indoor antenna can bring the signal out from a desk or out of a closet. In adjacent buildings, a roof antenna might be the answer.

In cities or congested areas, many people and pieces of equipment can be competing for the 2.4 GHz range. You may want to move a microwave oven or high-end remote phone that may be interfering with your wireless LAN. These settings may help adapt to poor reception:

- Reduce transmission rate — Instead of using 11 Mbps, you can explicitly ramp down to 5.5, 2, or 1 Mbps. Slower rates can mean more efficient operation in noisy places.
- Use smaller fragment sizes — Although there is more total overhead to transmitting packets broken up into smaller fragments, they can often provide better performance in noisy environments. Change the `frag` parameter to reduce fragment sizes.
- Use different frequencies — By specifically requesting certain frequencies (or channels) be used for transmission, you can avoid congested channels.

## Debugging tools

Because some wireless LAN cards were created for Windows systems, debugging tools from the manufacturers are available only on those systems. If your computer is a dual-boot system (Windows and Linux), try booting in Windows to test the quality of your wireless network.

In Fedora and RHEL, you can use many of the tools for used Ethernet networks and other TCP/IP network interfaces. Here are a couple of examples:

- **Wireshark** — The Wireshark (type `wireshark` as root user from a Terminal window) lets you watch Ethernet being sent and received by your wireless LAN interface. For example, the output of Wireshark can tell you whether a failed connection reflects a lack of reception or rejected requests. (Wireshark is described in the next section).
- **/var/log/messages** — When the wireless LAN interface starts up, messages related to that are sent to the `/var/log/messages` file. In some cases, these messages will reflect improper options being for the wireless LAN module.

## Watching LAN traffic with Wireshark

If you really want to understand the coming and going of information on your LAN, you need a tool that analyzes network traffic. Wireshark (formerly called Ethereal) is a graphical tool for capturing and displaying the packets being sent across your network interfaces. Using filters to select particular hosts, protocols, or direction, you can monitor activity.

In addition to reading packet data gathered by Wireshark, the Wireshark window can be used to display packets from LanAnalyzer, Sniffer, Microsoft Network Monitor, Snoop, and other tools. These files can be read from their native formats or after being compressed with gzip.

Wireshark can track more than 100 packet types (representing protocols). It can also display specific fields related to each protocol, such as various data sizes, source and destination addresses, port numbers, and other values.

### Starting Wireshark

To start Wireshark from the Applications menu, select Internet -> Wireshark. Or type the following (as root) from a Terminal window:

# Part IV: Fedora RHEL Network and Server Setup

The Wireshark window, shown in Figure 15-1. (If the wireshark command is not found, the package is probably not installed. You can install the wireshark and wireshark-common packages from the Internet typing yum install wireshark wireshark-gnome, or you can use the rpi command to install them from the installation DVD.)

![](img/63c86e1d25a0e2be7e9f6de6b6f02530_727_0.png)

Figure 15-1: Wireshark captures and displays data on a network interface.

> TIP: If you cannot use Wireshark because you don't have a GUI application, you can use the tcpdump command from the shell. It is not as friendly as Wireshark, but it supports the filtering syntax. tcpdump can produce a lot of output, you will probably want to use some form of filtering or direct the output of the command to a file. (Type tcpdump for information on filter options.)
