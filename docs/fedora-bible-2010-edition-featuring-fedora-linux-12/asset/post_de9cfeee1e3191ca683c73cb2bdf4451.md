
## Troubleshooting a wireless LAN

If you set up your two (or more) wireless LAN cards to enable Fedora systems to communicate, and they are not communicating, you can troubleshoot the problem in several different ways.

## Checking wireless settings

You can use the `iwlist` and `iwconfig` commands to check your wireless settings. The `iwconfig` command provides a quick overview of your wireless settings, while the `iwlist` command shows you information about parameters that you specify.

Use the `iwconfig` command, along with the name of the wireless LAN interface, to see information about that interface. For example, if the wireless interface were `eth1`, you could type the following:

```bash
# iwconfig eth1
eth0    IEEE 802.11-DS  ESSID:"Houelan"  Nickname:"pine"
        Mode:Ad-Hoc  Frequency:2.412GHz  Cell: 02:02:2D:2D:3B:30
        Bit Rate=11Mb/s   Tx-Power=15 dBm   Sensitivity:1/3
        RTS thr:off   Fragment thr:off
        Encryption key:7365-6375-31
        Power Management:off
        Link Quality:0/92  Signal level:-102 dBm  Noise level:-102 dBm
        Rx invalid nwid:0  invalid crypt:0  invalid misc:0
```

With `iwconfig`, you can see details about the wireless aspects of the Ethernet interface. In this example, the network name (ESSID) is `Houelan`, and the station name (Nickname) is `pine`. The interface is operating in Ad hoc mode on channel 1 (frequency of 2.412 GHz). Transmission rates are at the maximum speed of 11 Mbps. The encryption key that must be used by every node the card connects with is `7365-6375-31`. Other settings describe the link and signal quality.

The `iwlist` command lets you request specific information about the wireless LAN interface. The syntax is to follow the `iwlist` command with the interface name and the information you are interested in. For example:

```bash
# iwlist eth1 freq
eth0   14 channels in total; available frequencies :
       Channel 01 : 2.412 GHz
       Channel 02 : 2.417 GHz
       Channel 03 : 2.422 GHz
       Channel 04 : 2.427 GHz
       Channel 05 : 2.432 GHz
       Channel 06 : 2.437 GHz
       Channel 07 : 2.442 GHz
       Channel 08 : 2.447 GHz
       Channel 09 : 2.452 GHz
       Channel 10 : 2.457 GHz
       Channel 11 : 2.457 GHz
       Channel 12 : 2.457 GHz
       Channel 13 : 2.457 GHz
       Channel 14 : 2.462 GHz
Current Frequency:2.412GHz (Channel 1)
```

The `freq` parameter displays the frequencies (and channels) available for communication. Note that all the available frequencies are in the 2.4 GHz range.

```bash
# iwlist eth0 rate
eth0    6 available bit-rates :
        1Mb/s
        2Mb/s
        5.5Mb/s
        11Mb/s
        58Mb/s
        39.5Mb/s
Current Bit Rate=54Mb/s
```

The preceding `rate` parameter displays the transmission rates available for the wireless interface. You can see that 1, 2, 5.5, and 11 Mbps rates are available for the current interface.

```bash
# iwlist eth0 key
eth0    2 key sizes : 40, 104bits
4 keys available :
[1] 7365-6375-31 (40 bits)
[2] off
[3] off
[4] off
Current Transmit Key: [1]
```

The `key` parameter lets you see the encryption keys available with the interface. It also shows the key sizes currently available. Because the card reflected in the preceding example supports 64- and 128-bit encryption, the key sizes available are 40 and 104 bits. (The encryption algorithm automatically generates the last 24 bits of each key.)

If you are troubleshooting your wireless LAN connection, some settings are more likely than others to cause problems. It is important to set the following wireless LAN settings properly — if you don’t, they may keep your network from working:

- **Network ID (ESSID)** — You may not be able to communicate among peer computers if the Network ID, also called network name or ESSID, doesn’t match on each of them. Network IDs are case sensitive — for example, `MyLAN` is not the same as `mylan`.
- **Encryption key** — Having encryption keys that don’t match is like trying to log in to Linux with the wrong password. Check that all nodes are using the same key. (If nodes were unable to connect, check the encryption key first because typing long hexadecimal keys can be prone to error.)
- **Mode** — If you are communicating through an access point, your mode should be set to Managed and you must provide the MAC address for that access point. In most single-cell networks, you should set all nodes to Ad hoc. The Ad hoc mode allows all nodes to communicate directly to each other as peers.
- **Channel or frequency** — The channel and frequency options are just two different means of setting the same value. For example, setting the channel to 1 is the same as setting the frequency to 2.412G (GHz). Make sure that the nodes on your network are able to communicate on the same frequency.

## Checking TCP/IP

To ensure that your wireless LAN is communicating with its peers, use the `ping` command (as described earlier in this chapter). If you believe that your cards are working properly, but the `ping` command continues to give you a `Network Unreachable` message, you may have a problem with your TCP/IP configuration. Here are some items you can check from the Network Configuration window:

- **IP address** — Know the correct IP address of the peer you are trying to reach.
- **Hostname** — If you ping the peer computer by name, make sure that your computer can properly resolve that name into the correct IP address, or have the peer’s hostname and IP address properly listed in the `/etc/hosts` file locally. The former option will probably require that you have one or more DNS servers identified to resolve the name.

If you can reach another computer on the wireless LAN, but not computers outside of that LAN (such as Internet addresses), check that you have properly identified the location of your gateway. If the gateway address is correct, and you can reach that gateway, it may be that the gateway itself is not configured to allow packet forwarding.

> **NOTE:** On the computer that is acting as a gateway from your wireless network to the Internet, you need to turn on IP packet forwarding. Change the value of `net.ipv4.ip_forward` to 1 in `/etc/sysctl.conf`. Open that file as the root user with a text editor and change the line as follows:
>
> ```
> net.ipv4.ip_forward = 1
> ```

If you found that any of the preceding information needed to be changed and you changed it, you should restart the wireless LAN interface. One way to do that is to restart the network interface as follows:

```bash
# service network restart
```

## Adapting to poor reception

Your wireless LAN might be working fine while your two wireless computers are sitting on the same desk. But if performance degrades when you separate the computers, you may need to identify any potential obstructions. Then you must decide how to get around them. For desktop systems, a small indoor antenna can bring the signal out from under a desk or out of a closet. For adjacent buildings, a roof antenna might be the answer.

In cities or other congested areas, many people and pieces of equipment can be competing for the 2.4 GHz range. You may want to move a microwave oven or high-end remote phone that may be interfering with your wireless LAN. These settings might help adapt to poor reception:

- **Reduce transmission rate** — Instead of using 11 Mbps, you can explicitly ramp down to 5.5, 2, or 1 Mbps. Slower rates can mean more efficient operation in noisy places.
- **Use smaller fragment sizes** — Although there is more total overhead to transmitting packets broken up into smaller fragments, they can often provide better overall performance in noisy environments. Change the `frag` parameter to reduce fragment sizes.
- **Use different frequencies** — By specifically requesting that certain frequencies (or channels) be used for transmission, you can avoid congested channels.

## Use debugging tools

Because most wireless LAN cards were created for Windows systems, debugging tools from the manufacturers are available only on those systems. If your computer is a dual-boot system (Windows and Linux), try booting in Windows to test the quality of your wireless network.

In Fedora, you can use many of the tools you use for wired Ethernet networks and other TCP/IP network interfaces. Here are a couple of examples:

- **Wireshark** — The Wireshark window (type `wireshark` as the root user from a Terminal window) lets you watch Ethernet frames being sent and received by your wireless LAN interface. For example, the output of Wireshark can tell you whether a failed connection reflects a lack of reception or rejected requests. (Wireshark is described in the next section.)
- **/var/log/messages** — When the wireless LAN interface starts up, messages related to that startup are sent to the `/var/log/messages` file. In some cases, these messages will reflect improper options being set for the wireless LAN module.

## Watching LAN traffic with Wireshark

If you really want to understand the coming and going of information on your LAN, you need a tool that analyzes network traffic. Wireshark (formerly called Etheral) is a graphical tool for capturing and displaying the packets being sent across your network interfaces. Using filters to select particular hosts, protocols, or direction of data, you can monitor activities and track problems on your network.

In addition to reading Ethernet packet data gathered by Wireshark, the Wireshark window can be used to display captured files from LanAlyzer, Sniffer, Microsoft Network Monitor, Snoop,
