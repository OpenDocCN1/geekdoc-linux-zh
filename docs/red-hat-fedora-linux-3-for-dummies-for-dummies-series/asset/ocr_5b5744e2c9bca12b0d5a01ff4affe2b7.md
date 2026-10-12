look at these files to gain an understanding of how Linux works. Display the networking devices by typing this command:

```
`cat /proc/net/dev`
```

If you don't see the Ethernet interface, you may have an unsupported network adapter or a defective or misconfigured one. The Fedora Core kernel, by default, automatically loads modules as they're needed. You can look back at the results of your boot process by using the `dmesg` command. Look for a message that says `delaying eth0 configuration`. This message probably means that Linux couldn't load the network adapter module or that the adapter isn't working.

Display the information about your devices by using the `cat /proc/net/dev` command.

The next step is to ensure that your network routing is configured correctly. This area is one where you can easily get confused. You don't have to set up routing outside your LAN yet, but Linux needs to know where to send packets on its own network. Look at your routing table by typing this command:

```
`netstat -nr`
```

You see a listing of your routing table. In this abbreviated example, some options that aren't important have been removed:

```
Kernel IP routing table
Destination     Gateway         Genmask         Flags   Iface
192.168.1.0     0.0.0.0         255.255.255.0   U         eth0
169.254.0.0     0.0.0.0         255.255.0.0     U         eth0
127.0.0.0       0.0.0.0         255.0.0.0       U         lo
0.0.0.0         192.168.1.254   0.0.0.0         UG        eth0
```

This list briefly describes what's in the fields in the routing table:

+   * **Destination:** The location, or IP address, where you want to send packets. For example, the address `192.168.1.0` refers to your local network.

+   * **Gateway:** The address (computer or router) where the packets have to be sent so they can find their way to their destination. When the destination is the local network, the address `0.0.0.0` means no gateway.

+   * **Genmask:** Used to separate from the host number the parts of the IP address used for the network address.

+   * **Flags:** Indicates various interface information. such as `U` for `up` and `G` for `gateway`. The metric is used as a measure of how far a packet must travel to its destination (a number greater than 32 is considered infinite; packets live in a small universe). The next two flags, Ref and Use, aren't important here.