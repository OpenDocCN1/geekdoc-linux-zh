
## Checking wireless settings

You can use the `iwlist` and `iwconfig` commands to check your wireless settings. The `iwconfig` command gives you a quick overview of your wireless settings, while the `iwlist` command shows you information about parameters you specify.

Use the `iwconfig` command, along with the name of the wireless LAN interface, to see information about that interface. For example, if the wireless interface were eth0, you could type the following:

```
# iwconfig eth0
eth0      IEEE 802.11-DS  ESSID:"Homelan"  Nickname:"pine"
          Mode:Ad-Hoc  Frequency:2.412GHz  Cell: 02:02:2D:2D:3B:30
          Bit Rate:11Mb/s  Tx-Power=15 dBm  Sensitivity:1/3
          RTS thr:off  Fragment thr:off
          Encryption key:7365-6375-31
          Power Management:off
          Link Quality:0/92  Signal level:-102 dBm  Noise level:-102 dBm
          Rx invalid nwid:0  invalid crypt:0  invalid misc:0
```

With `iwconfig`, you can see details about the wireless aspects of the Ethernet interface. In this example, the network name (ESSID) is Homelan, and the station name (Nickname) is pine. The interface is operating in Ad-hoc mode on channel 1 (frequency of 2.412 GHz). Transmission rates are at the maximum speed of 11 Mbps. The encryption key that must be used by every node the card connects with is 7365-6375-31. Other settings describe the link and signal quality.

The `iwlist` command lets you request specific information about the wireless LAN interface. The syntax is to follow the `iwlist` command with the interface name and the information you are interested in. For example:

```
# iwlist eth0 freq
eth  0    14 channels in total; available frequencies :
        Channel  01 : 2.412 GHz
        Channel  02 : 2.417 GHz
        Channel  03 : 2.422 GHz
        Channel  04 : 2.427 GHz
        Channel  05 : 2.432 GHz
        Channel  06 : 2.437 GHz
        Channel  07 : 2.442 GHz
        Channel  08 : 2.447 GHz
        Channel  09 : 2.452 GHz
        Channel  10 : 2.457 GHz
        Channel  11 : 2.462 GHz
```

The `freq` parameter displays the available frequencies (and channels) available for communication. Note that all the available frequencies are in the 2.4 GHz range.

```
# iwlist eth0 rate
eth0          4 available bit-rates :
              1 Mb/s
              2 Mb/s
              5.5 Mb/s
              11 Mb/s
```

The preceding rate parameter enables you to display the transmission rates available for the wireless interface. As you can see, the 1, 2, 5.5, and 11 Mbps rates are all available for the current interface.

```
# iwlist eth0 keys
eth0          2 key sizes : 40, 104bits
              4 keys available :
                  [1] 7365-6375-31 (40 bits)
                  [2] off
                  [3] off
                  [4] off

              Current Transmit Key: [1]
```

The keys parameter lets you see the encryption keys available with the interface. It also shows the key sizes currently available. Because the card reflected in the preceding example supports 64- and 128-bit encryption, the key sizes available are 40 and 104 bits. (The encryption algorithm automatically generates the last 24 bits of each key.)

If you are troubleshooting your wireless LAN connection, some settings are more likely than others to be causing problems. It is important to set the following wireless LAN settings properly — if you don’t, they may keep your network from working:

- **Network ID (ESSID)** — You may not be able to communicate among peer computers if the Network ID (ESSID) doesn’t match on each of them. Case is important — for example, MyLan is not the same as MyLAN.
- **Encryption key** — Having encryption keys that don’t match is like trying to log in to Linux without a password. Check that all nodes are using the same key.
- **Mode** — If you are communicating through an access point, your mode should be set to Managed and you must provide the MAC address for that access point. In most single-cell networks, you should set all nodes to Ad hoc. The Ad hoc mode allows all nodes to communicate directly to each other as peers.
- **Channel or Frequency** — The channel and frequency options are just two different means of setting the same value. For example, setting the channel to 1 is the same as setting the frequency to 2.412G (GHz). Make sure that the nodes on your network are able to communicate on the same frequency.

## Checking TCP/IP

To make sure that your wireless LAN is communicating with its peers, use the ping command (as described earlier in this chapter). If you believe that your cards are working properly, but the ping command continues to give you a “Network Unreachable” message, there may be a problem with your TCP/IP configuration. Here are some items you can check from the Network Configuration window:

- **IP address** — Make sure you know the correct IP address of the peer you are trying to reach.
- **Host name** — If you are pinging the peer computer by name, make sure that your computer can properly resolve that name into the correct IP address, or have the peer’s host name and IP address properly listed in the /etc/hosts file locally. The former option will probably require that you have one or more DNS servers identified to resolve the name.

If you are able to reach another wireless computer on the wireless LAN, but are not able to reach computers outside of that LAN (such as Internet addresses), check that you have properly identified the location of your gateway. If the gateway address is correct, and you can reach that gateway, the problem may be that the gateway itself is not configured to allow packet forwarding.

If you find that any of the preceding information needed to be changed and you changed it, you should restart the wireless LAN interface. One way to do that is to restart the PCMCIA interface and the network interfaces as follows:

```
# /etc/init.d/pcmcia restart
# /etc/init.d/network restart
```

## Adapting to poor reception

Your wireless LAN might be working fine while your two wireless computers are sitting on the same desk. But if performance degrades when you separate the computers, you may need to determine if there are obstacles in the way and, if so, how to get around them. For desktop systems, a small indoor antenna can bring the signal out from under a desk or out of a closet. For adjacent buildings, a roof antenna might be the answer.

In cities or other congested areas, many people and pieces of equipment can be competing for the 2.4 GHz range. You may want to move a microwave oven or high-end remote phone that may be interfering with your wireless LAN. Here are a few settings you can use to adapt to poor reception:

- **Reduce transmission rate** — Instead of using 11 Mbps, you can explicitly ramp down to 5.5, 2, or 1 Mbps. Slower rates can mean more efficient operation in noisy environments.
- **Use smaller frame sizes** — Though there is more total overhead to transmitting smaller frames, they can often provide better overall performance than large frames. Failures during transmissions of large frames cause smaller hits than failures during transmissions of small frames.
- **Use different frequencies** — You can specifically request that certain frequencies (or channels) be used for transmission. You can use this technique to avoid congested channels.

## Use debugging tools

Because Orinoco cards and most other wireless LAN cards were created for Windows systems, some of the better debugging tools are available only on those systems. If your computer is a dual-boot system (Windows and Linux), you can try booting in Windows to test the quality of your wireless network. For Orinoco cards in particular, you should run the Client Manager to view information about the quality of your wireless links.

In Red Hat Linux, you can use many of the tools you use for wired Ethernet networks and other TCP/IP network interfaces. Here are a couple of examples:

- **Ethereal** — The Ethereal window (type *ethereal* as the root user from a terminal window) enables you to watch Ethernet frames as they are sent and received by your wireless LAN interface. For example, the output of Ethereal can tell you whether a failed connection reflects a lack of reception or rejected requests. (Ethereal is described in the next section.)
- **/var/log/messages** — When the wireless LAN interface starts up, messages related to that startup are sent to the */var/log/messages* file. In some cases, these messages will reflect improper options being set for the wireless LAN module.

## Watching LAN traffic with Ethereal

If you really want to understand the coming and going of information on your LAN, you need a tool that analyzes network traffic. Ethereal is a graphical tool for capturing and displaying the packets being sent across your network interfaces. Using filters to select particular hosts, protocols, or direction of data, you can specifically monitor activities and track down problems on your network.

In addition to reading Ethernet packet data gathered by Ethereal, the Ethereal window can be used to display captured files from Lanalyzer, Sniffer, Microsoft Network Monitor, Snoop, and a variety of other tools. These files can be read from their native formats or after being compressed with gzip (.gz).

Ethereal can track more than 100 packet types (representing different protocols). It can also display specific fields related to each protocol, such as various data sizes, source and destination addresses, port numbers and other values.
