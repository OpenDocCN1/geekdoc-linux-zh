# Chapter 15: Setting Up Network Connections and LANs 675

If the eth0 interface does not appear, it may still be configured properly, but not running at the moment. Try to start the eth0 interface by typing the following:

```
# ifconfig eth0
```

After this, type ifconfig again to see if eth0 is now running. If it is, it may be that eth0 is simply not configured to start automatically at boot time. You can change it so Ethernet starts at boot time (which I recommend), using the Network Configuration window described earlier in this chapter.

> TIP: If your network interfaces are not running at all, you can try to start them from the network initialization script. This interface reads parameters and basically runs ifconfig for all network interfaces on your computer. Type the following to restart your network:

```
# /etc/init.d/network restart
```

Another way to see statistics for your Ethernet driver is to list the contents of the process pseudo system for network devices. Do that, by following:

```
# cat /proc/net/dev
```

The output should look like:

| face | Receive bytes packets fifo err drop drop fifo frame compressed multicast | Transmit bytes |
|---|---|---|---|---|---|---|---|---|---|---|\| lo: | 5362 | 64 | 0 | 0 | 0 | 0 | 5326 | 64 | 0 | 0 | 0 |
| sit0: | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| eth0: | 3083 | 35 | 0 | 0 | 0 | 0 | 0 | 3876 | 31 | 0 | 0 | 0 |

The output is a bit hard to read. (This book isn't wide enough to show it wrapping around, so the output is truncated.) With this output, you can see Receive and Transmit statistics for each interface. This output also shows how many Receive and Transmit errors occur in communication. (Transmit information is cut off in this example.)

For a more detailed look at your network, you can use the Wireshark window. Wireshark is described in the section “Watching LAN traffic with Wireshark” later in this chapter.

> NOTE: sit0 interface (which stands for Simple Internet Transition) can be used to encapsulate IPv6 packets into an IPv4 network. This allows IPv6 communications to be routed across IPv4 networks. You would only use this interface if you have IPv6 enabled.

# Troubleshooting a wireless LAN

If you set up two (or more) wireless LAN cards to enable Fedora and RHEL systems to communicate, and they are not communicating, you can troubleshoot the problem in several ways.