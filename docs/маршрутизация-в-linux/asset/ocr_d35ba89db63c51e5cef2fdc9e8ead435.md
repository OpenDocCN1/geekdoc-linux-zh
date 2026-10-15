IPaddr tells phyint which physical interface you're referring to and can be an IP address or an interface name, such as eth0. After this, you have a collection of options that you can add to suit your needs:

+   - **disable**. Indicates to route no DVMRP traffic through this interface.
+   - **metric metric**. The cost for sending data from the multicast source to this interface. For an interface to be valid, the metric should be below 31. It's often recommended to use 1.
+   - **threshold threshold**. The minimum Internet Protocol (IP) time-to-live setting the packet must have before mrouted will bother sending this packet along to the interface. This value is given in seconds.
+   - **rate_limit rate_limit**. The rate in Kbits/second that this interface will accept multicast traffic, if you want to limit this.
+   - **boundary boundaryname**. Apply this set of rules to the network block defined earlier with the name statement. You can have more than one of these options.
+   - **boundary boundaryadd/masklen**. Apply this set of rules to the network block specified by these variables, which are utilized in the same way you would use them in the name statement. You can have more than one of these options.
+   - **altnet subnet/masklen**. If the interface in question leads to a number of subnets, you can refine the data path utilizing this option. subnet refers to the network address for the specific subnet you want to set up, and masklen is the same as it is defined in the name statement. You can have more than one of these options.
+   - **altnet subnet**. If the interface in question leads to a number of subnets, you can refine the data path utilizing this option. subnet refers to the network address for the subnet you want to set up and assumes that there is no netmask needed. You can have more than one of these options.

Now we finally get into an order issue. The final possibility here is the tunnel statement, which you can utilize to set up a unicast method of transporting your multicast data from one mrouted machine to another across unicast-only network space. You must define your tunnels after your physical interfaces. The base format for this item is tunnel local remote

As you might guess, local refers to the connected interface on which to start the tunnel—either an IP address or device name—and remote refers to the IP address of the interface to connect to on the other end to receive the data. All of the additional options are identical to those available in phyint: metric, threshold, rate_limit, boundary boundaryname, and boundary boundaryadd/masklen. See the previous bulleted list for definitions of these options and how to set them.

For example, I might set up my configuration file to be as close as possible to the PIM-SM configuration file as follows:

```
name multi 199.60.103.0/32
cache_lifetime 21600
```