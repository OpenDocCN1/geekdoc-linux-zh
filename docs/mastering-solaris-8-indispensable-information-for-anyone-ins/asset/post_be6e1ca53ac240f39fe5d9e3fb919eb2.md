
## FIGURE 9.11

The Telnet remote utility

![](img/256e02a6afce528d264a8d911fa0ff20_392_0.png)

If you connect to a remote Solaris system through Telnet, you will see a regular login prompt. On the other hand, rlogin naturally assumes that the login name on the remote system matches that on your local system. Because Telnet is specifically designed to work with non-Unix systems, it does not make such assumptions. To specify a different login name with rlogin, use the -l option.

> **TIP Security is an issue when you use rlogin or Telnet. Your password can be read by others who tune into the session. Refer to Chapter 8, “Security,” for more information.**

Telnet allows you to configure special parameters such as how returns or interrupts are processed. However, if you are using Telnet between two Unix/Solaris systems, it is rare to have to change any parameters. You should specify the name of a remote host on the command line. Telnet will run in interactive mode if you do not.

Before Telnet connects you to a remote system, it will tell you what your escape character will be. Most often it will be the `Ctrl+\`. If you enter a question mark in response to the `telnet>` prompt, Telnet displays a help list of the commands it recognizes. The `close` command ends the current Telnet session. To release out of Telnet’s interactive mode and return to communicating with the remote system, press Return in response to a prompt.

> **TIP** You can use remote services at special sites such as LOCIS, which is the U.S. Library of Congress Information System.

If you want to determine how long a system has been up and running, as well as the load average, use the `rup <systemname>` command. This command displays host name and uptime and load averages. You can also determine whether a system is connected and responding using the `ping` command, which is described in the following section. The third important command that is useful to determine system status on a network is the `rpcinfo` command. This command, typically issued in the form `rpcinfo -p <systemname>`, returns information about the RPC (daemon) services.

## The ping Utility

To test a network connection or to verify that a remote system is available, the `ping` utility is used. It sends a special kind of IP data packet to the remote computer to elicit a reply. This is usually the fastest way to verify that a remote system is available and to check whether the network is operating efficiently. The `ping` utility uses a protocol called ICMP, or Internet Control Message Protocol.

The name `ping` mimics the sound of a sonar burst used by submarines to communicate with each other. Without any options, `ping` will test the connection to the remote system once and send back a reply.

> **TIP** If you use the `-o` option and `ping` is unable to connect to the remote system, it will continue to try until you interrupt it with **Ctrl+C**. A failure to get a reply indicates that the system may be down or may be experiencing a software failure.

If, however, a system responds to `ping`, it does not necessarily mean that it is functional. Quite often a system will hang to the point where it no longer responds to Telnet/Web/FTP-type requests but will still respond to `ping`.

By default, the `ping` utility sends packets containing 64 bytes: 56 data bytes and 8 bytes of protocol header information. A packet sequence number called `icmp_seq` is also given. You can tell if a packet is dropped because a gap will occur in the sequence numbers. The round-trip time is listed in milliseconds and appears last in line. It represents the time it took for the packet to get from the local system to the remote system and for the reply to get from the remote system back to the local system. Distance between the two systems affects the time as well as other network traffic and the load on both systems.

If a host is unreachable, the ping utility will appear to hang because a timeout is occurring. The timeout will expire after it listens for a response from the remote system. The ping utility will ultimately inform you that the host is unreachable. If you try several different timeout values and you are unable to contact the remote system, try to ping other systems to determine where the problem originates. The default timeout is 20 seconds, but you can specify a different timeout. The following example displays the syntax:

```
   % ping <host> <timeout>
```

In this example, <host> is the host name or IP address of the system you want to contact, and <timeout> is the timeout in seconds. On occasion, you may try to contact a host that is extremely slow. You should increase the timeout in order for your system to receive a response. Try the following example and reset the timeout to 30 seconds:

```
   % ping delphi 30
```

There are times when reaching a host is a problem. Sometimes you will have periods of good connectivity and then will encounter a few intermittent instances of unreachability. To determine the problem, you can keep trying to ping a host by using the -s option, as in the following example:

```
   % ping -s <host>
```

This causes the ping utility to send an ICMP echo request message to the remote system every second. Once it makes a connection, the ping utility will summarize the results and display how many packets were sent and received. It will display the minimum, average, and maximum round-trip delays it measured as well.

There will be times when you find that you are unable to connect to a remote system using Telnet. When you use the ping utility, however, you do get a response back. To debug this problem, you need to verify that the remote system is reachable for larger packets. Once you verify that you can send large packets to the remote system, you can use the telnet command to test whether the protocol is running on the remote system. Usually, the ping command sends small packets to the remote systems. If a network has heavy traffic and the systems are loaded, they can still respond to the ping. Larger packets may not reach the remote system or may be dropped in transit. You can test this by using the ping utility as displayed here:

```
   % ping -s <host> <size>
```

In this example, <host> is the host name or IP address of the remote system and <size> is the size in bytes of the packet you wish to send. It's common to use 4,096 bytes per packet, and 512 bytes, 1,024 bytes, 4,092 bytes, and 8,096 bytes are also common packet sizes to try when testing to see if a remote system is receiving. Ethernet systems typically take the 1,024-byte packets. It is also possible to specify the number of packets that should be sent to the remote system by using the following syntax:

```
% ping -s <host> <size> <count>
```

When the number of packets has been specified, ping will exit and print a summary after it has finished transmitting the number you requested. You do not have to quit the program by pressing Ctrl+C. You will find this feature useful for hosts who are difficult to reach. The following example is the ping command requesting a try every second (-s) on the host Delphi, with 1,024-byte packets for 3 packets:

```
% ping -s delphi 1024 3
```

## The arp Utility

All systems store a mapping table of IP addresses to Media Access Control (MAC) addresses for systems on their local network. This table is called the Address Resolution Protocol cache, or the ARP cache. The table is updated frequently by the Address Resolution Protocol (ARP), and the updates are based on the presence or absence of a MAC address in the broadcast traffic. Because of this, ARP is usually associated with Ethernet networks. It can be available on Token Ring and FDDI networks as well. If an address is not present in the ARP cache when it is requested by the system, ARP will create a message requesting the mapping and broadcast it on the network. When a response is received, the new mapping is added to the ARP table and any waiting messages to the remote host are forwarded. ARP will broadcast four messages before reporting a failure.

Solaris has an arp utility that allows you to view all of the entries in the ARP cache on your system. Figure 9.12 shows the output from the arp command. The syntax to use is % arp -a.

```
% arp -a
```

The first column specifies the interface that was used to learn the MAC address. The second and third columns contain the host name and network mask of the system that corresponds to the MAC address. The fourth column displays a set of flags that indicate the state of the entry. The fifth column contains the actual MAC address of the host system. If you needed to find all of the ARP entries that share a similar type of Ethernet card or are within a certain domain, you can combine the arp command with the grep command as in the following example:

```
% arp -a | grep <param>
```

In this example, the parameter you are interested in looking for is in the output. The following example shows the syntax for printing out all of the ARP cache entries for hosts in the delphi.us domain:

```
% arp -a | grep delphi.us
```

![](img/256e02a6afce528d264a8d911fa0ff20_395_0.png)
