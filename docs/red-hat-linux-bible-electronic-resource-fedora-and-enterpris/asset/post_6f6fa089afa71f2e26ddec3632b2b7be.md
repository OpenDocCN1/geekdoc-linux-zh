
```
64 bytes from pine (10.0.0.10): icmp_seq=10 ttl=255 time=0.367 ms
--- ping statistics ---
10 packets transmitted, 10 packets received, 0% packet loss, time 9011ms
rtt min/avg/max/mdev = 0.351/0.402/0.457/0.042 ms
```

A line of output is printed each time a packet is sent and received in return. It shows how much data was sent and how long it took for each packet to be received. After you have watched this for a while, type Ctrl+C to stop ping. At that point, you will see statistics on how many packets were transmitted, received, and lost

If you don't see output that shows packets have been received, it means you are not contacting the other computer. Try to verify that the names and addresses of the computers that you want to reach are in your /etc/hosts file or that your DNS server is accessible. Next, confirm that the names and IP addresses you have for the other computers you are trying to reach are correct (the IP addresses are the most critical).

## Is your Ethernet connection up?

Using the ifconfig command, you can determine whether your Ethernet (and other network interfaces) are up and running. Type the following command:

```
# ifconfig
```

The output that appears is similar to the following:

```
eth0 Link encap:Ethernet HWaddr 00:90:27:4E:67:35
    inet addr:10.0.0.10 Bcast:10.0.0.255 Mask:255.255.255.0
    UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1
    RX packets:156 errors:0 dropped:0 overruns:0 frame:0
    TX packets:104 errors:0 dropped:0 overruns:0 carrier:0
    collisions:0 txqueuelen:100
    RX bytes:20179 (19.7 Kb)   TX bytes:19960 (19.4 Kb)
    Interrupt:11 Base address:0xe000 Memory:ff8ff000-ff8ff038

lo    Link encap:Local Loopback
    inet addr:127.0.0.1 Mask:255.0.0.0
    UP LOOPBACK RUNNING MTU:3924 Metric:1
    RX packets:56 errors:0 dropped:0 overruns:0 frame:0
    TX packets:56 errors:0 dropped:0 overruns:0 carrier:0
    collisions:0 txqueuelen:0
    RX bytes:3148 (3.0 Kb)    TX bytes:3148 (3.0Kb)
```

In this example, two network interfaces are up on the current computer. The first section shows your Ethernet interface (eth0), and its Ethernet hardware address, IP address (inet addr), broadcast address, and network mask. The next lines provide information on packets that have been sent, along with the number of errors and collisions that have occurred.

> **NOTE:** The `lo` entry is for loopback. This enables you to run TCP/IP commands on your local system without having a physical network up and running.

If your `eth0` interface does not appear, it may still be configured properly, but not running at the moment. Try to start the `eth0` interface by typing the following:

```
# ifconfig eth0 up
```

After this, type `ifconfig` again to see if `eth0` is now running. If it is, it may be that `eth0` is simply not configured to start automatically at boot time. You can change it so Ethernet starts at boot time (which I recommend), using the Network Configuration window described earlier in this chapter.

> **TIP:** If your network interfaces are not running at all, you can try to start them from the network initialization script. This interface reads parameters and basically runs `ifconfig` for all network interfaces on your computer. Type the following to restart your network:

```
# /etc/init.d/network restart
```

Another way to see statistics for your Ethernet driver is to list the contents of the process pseudo file system for network devices. To do that, type the following:

```
# cat /proc/net/dev
```

The output should look like this:

| Interface | bytes | packets | errs | drop | fifo | frame | compressed | multicast | bytes | packets | errs | drop | fifo | frame | compressed | multicast |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| lo: | 5362 | 64 | 0 | 0 | 0 | 0 | 0 | 5362 | 64 | 0 | 0 | 0 |  |  |  |  |
| eth0: | 3083 | 35 | 0 | 0 | 0 | 0 | 0 | 3876 | 31 | 0 | 0 | 0 |  |  |  |  |

The output is a bit hard to read (our book isn't wide enough to show it without wrapping around, so the output was truncated at the right). With this output, you can see Receive and Transmit statistics for each interface. This output also shows you how many Receive and Transmit errors occurred in communication. (Transmit information is cut off in this example.)

For a more detailed look at your network, you can use the Ethereal window. Ethereal is described in the "Watching LAN traffic with Ethereal" section later in this chapter.

## Troubleshooting a wireless LAN

If you set up your two (or more) wireless LAN cards to enable Red Hat Linux systems to communicate, and they are not communicating, you can troubleshoot the problem in several different ways.

### Checking wireless settings

You can use the iwlist and iwconfig commands to check your wireless settings. The iwconfig command provides a quick overview of your wireless settings, while the iwlist command shows you information about parameters that you specify.

Use the iwconfig command, along with the name of the wireless LAN interface, to see information about that interface. For example, if the wireless interface were eth1, you could type the following:

```
# iwconfig eth1
eth0    IEEE 802.11-DS  ESSID:"Homedlan"  Nickname:"pine"
      Mode:Ad-Hoc  Frequency:2.412GHz  Cell: 02:02:2D:2D:3B:30
      Bit Rate=11Mb/s  Tx-Power=15 dBm  Sensitivity:1/3
      RTS thr:off    Fragment thr:off
      Encryption key:7365-6375-31
      Power Management:off
      Link Quality:0/92  Signal level:-102 dBm  Noise level:-102 dBm
      Rx invalid nwid:0  invalid crypt:0  invalid misc:0
```

With iwconfig, you can see details about the wireless aspects of the Ethernet interface. In this example, the network name (ESSID) is Homedlan, and the station name (Nickname) is pine. The interface is operating in Ad hoc mode on channel 1 (frequency of 2.412 GHz). Transmission rates are at the maximum speed of 11 Mbps. The encryption key that must be used by every node the card connects with is 7365-6375-31. Other settings describe the link and signal quality.

The iwlist command lets you request specific information about the wireless LAN interface. The syntax is to follow the iwlist command with the interface name and the information you are interested in. For example:

```
# iwlist eth0 freq
eth0     14 channels in total; available frequencies :  
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
      Channel 11 : 2.462 GHz
```

The freq parameter displays the available frequencies (and channels) available for communication. Note that all the available frequencies are in the 2.4 GHz range.

```
# iwlist eth0 rate
eth0    4 available bit-rates :
	1 Mb/s
	2 Mb/s
	5.5 Mb/s
	11 Mb/s
```

The preceding rate parameter displays the transmission rates available for the wireless interface. You can see that 1, 2, 5.5, and 11 Mbps rates are available for the current interface.

```
# iwlist eth0 keys
eth0    2 key sizes : 40, 104bits
	4 keys available :
		[1] 7365-6375-31 (40 bits)
		[2] off
		[3] off
		[4] off
	Current Transmit Key: [1]
```

The keys parameter lets you see the encryption keys available with the interface. It also shows the key sizes currently available. Because the card reflected in the preceding example supports 64- and 128-bit encryption, the key sizes available are 40 and 104 bits. (The encryption algorithm automatically generates the last 24 bits of each key.)

If you are troubleshooting your wireless LAN connection, some settings are more likely than others to cause problems. It is important to set the following wireless LAN settings properly — if you don't, they may keep your network from working:

- **Network ID (ESSID)** — You may not be able to communicate among peer computers if the Network ID (ESSID) doesn't match on each of them. Case is important — for example, Mylan is not the same as MyLAN.
- **Encryption key** — Having encryption keys that don't match is like trying to log in to Linux with the wrong password. Check that all nodes are using the same key.
- **Mode** — If you are communicating through an access point, your mode should be set to Managed and you must provide the MAC address for that access point. In most single-cell networks, you should set all nodes to Ad hoc. The Ad hoc mode allows all nodes to communicate directly to each other as peers.
- **Channel or frequency** — The channel and frequency options are just two different means of setting the same value. For example, setting the channel to 1 is the same as setting the frequency to 2.412G (GHz). Make sure that the nodes on your network are able to communicate on the same frequency.

### Checking TCP/IP

To ensure that your wireless LAN is communicating with its peers, use the ping command (as described earlier in this chapter). If you believe that your cards are working properly, but the
