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

| Inter- | | | | | | | | | | Transmit |
|---|---|---|---|---|---|---|---|---|---|---|
| face | bytes | packets | errs | drop | fifo | frame | compressed | multicast | bytes | |
| lo: | 5362 | 64 | 0 | 0 | 0 | 0 | 0 | 5362 | 64 | 0 | 0 | 0 |
| eth0: | 3083 | 35 | 0 | 0 | 0 | 0 | 0 | 3876 | 31 | 0 | 0 | 0 |

The output is a bit hard to read (our book isn't wide enough to show it without wrapping around, so the output was truncated at the right). With this output, you can see Receive and Transmit statistics for each interface. This output also shows you how many Receive and Transmit errors occurred in communication. (Transmit information is cut off in this example.)

For a more detailed look at your network, you can use the Ethereal window. Ethereal is described in the "Watching LAN traffic with Ethereal" section later in this chapter.

# ## Troubleshooting a wireless LAN

If you set up your two (or more) wireless LAN cards to enable Red Hat Linux systems to communicate, and they are not communicating, you can troubleshoot the problem in several different ways.