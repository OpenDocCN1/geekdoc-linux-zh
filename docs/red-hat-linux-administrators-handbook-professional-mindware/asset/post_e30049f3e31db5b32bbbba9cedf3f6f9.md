
get any replies from your ping attempts, go back to the beginning of this section and ensure that you have followed all the steps as suggested.

## Aliasing multiple IP addresses with a single network interface

The first step in creating an IP alias is to determine whether you have the IP alias module loaded with the kernel. The simplest way to check this is to run the `lsmod` command and see whether `ip_alias.o` is listed anywhere in the output. If you don't see this module and haven't custom-compiled your kernel to include this module as part of the kernel, you can try to load the module by using the following command:

```
/sbin/insmod /path/to/ip_alias.o
```

where `/path/to/ip_alias.o` is the real path to the `ip_alias.o` module. You can use `locate ip_alias.o` to locate the path in your system. Typically, the path is `/lib/modules/kernel_version_number/ipv4/ip_alias.o`. After you load the `ip_alias.o` module, run `lsmod` to ensure that it is loaded. Now, to create an alias for the `eth0` device, do the following:

- Copy your existing `/etc/sysconfig/network-scripts/ifcfg-eth0` file to `/etc/sysconfig/network-scripts/ifcfg-eth0:0` to create a new device named `eth0:0`.
- Modify the file so that you have lines similar to the ones shown in Listing 7-3. Of course your network, netmask, and IP address will vary. Make sure you change only the `DEVICE` and `IPADDR` lines. The `DEVICE` line should be set to `eth0:0`, and `IPADDR` should be set to the IP address you want to use as an alias to what you have assigned for `eth0`.

### Listing 7-3 The /etc/sysconfig/network-scripts/ifcfg-eth0:0 file

```
DEVICE=eth0:0
USERCTL=no
ONBOOT=yes
BOOTPROTO=
BROADCAST=206.171.50.63
NETWORK=206.171.50.48
NETMASK=255.255.255.240
IPADDR=206.171.50.58
```

- To start the alias device, run `ifconfig eth0:0 up`. You should see output similar to the following:

```
lo Link encap:Local Loopback
innet addr:127.0.0.1 Bcast:127.255.255.255
Mask:255.0.0.0
UP BROADCAST LOOPBACK RUNNING MTU:3584 Metric:1
RX packets:501 errors:0 dropped:0 overruns:0
frame:0
TX packets:501 errors:0 dropped:0 overruns:0
carrier:0
collisions:0
eth0 Link encap:Ethernet HWaddr 00:C0:F6:98:37:37
innet addr:206.171.50.50 Bcast:206.171.50.63
Mask:255.255.255.240
UP BROADCAST RUNNING MULTICAST MTU:1500
Metric:1
RX packets:2 errors:0 dropped:0 overruns:0
frame:0
TX packets:2 errors:0 dropped:0 overruns:0
carrier:0 collisions:4
Interrupt:5 Base address:0x340
eth0:0 Link encap:Ethernet HWaddr 00:C0:F6:98:37:37
innet addr:206.171.50.58 Bcast:206.171.50.63
Mask:255.255.255.240
UP BROADCAST RUNNING MTU:1500 Metric:1
RX packets:9 errors:0 dropped:0 overruns:0 frame:0
TX packets:9 errors:0 dropped:0 overruns:0 carrier:0 collisions:0
```

As you can see, the `eth0` device is up and running. You can create an alias of any other Ethernet device in the same way.

## Using netcfg to configure a network interface card

You need to have X Window System working on your system to use `netcfg`. This program allows you to configure all aspects of the basic network configuration. You must run this as a superuser from X Window System. The initial window, shown in Figure 7-5, displays the current hostname, domain name, and nameserver configuration.

![](img/f9ec99365f159bfe663f8ac29732663c_168_0.png)

Figure 7-5 The Names tab of the Network Configurator window

To change the hostname, the domain name, or the nameservers, first click the Names tab. Simply modify the values and click Save. The program doesn't display any status message when you click Save, so it's a bit confusing at first. Also, the domain name displayed in the program comes from the search list (first entry in the list) in the `/etc/resolv.conf` file, so if you don’t have any search list set up in this file, `netcfg` will not display any domain name.

To add, modify, or remove a network interface, click the Interfaces tab, shown in Figure 7-6, which displays the current network interfaces.

![](img/f9ec99365f159bfe663f8ac29732663c_169_0.png)

To add a new network interface, do the following:

- Click **Add** to bring up the Choose Interface Type dialog box, shown in Figure 7-7.

![](img/f9ec99365f159bfe663f8ac29732663c_169_1.png)

- Click **Ethernet** to create a new Ethernet network interface configuration. After you click **OK**, you will see the Edit Ethernet/Bus Interface dialog box, shown in Figure 7-8.

![](img/f9ec99365f159bfe663f8ac29732663c_170_0.png)

Figure 7-8 Entering information about the new interface

- Enter the IP address and the network mask for this new device. The `netcfg` program automatically calculates the network and broadcast addresses from the information you provide. If you want this interface to be active at boot time, click Activate interface at boot time. Leave the Allow any user to (de)activate interface option unchecked, because allowing just anyone to activate or deactivate your network interfaces is really a bad idea. If you are not using DHCP or BOOTP servers to dynamically assign IP addresses for this interface, select none as the interface configuration protocol. Click Done to complete the configuration; you will be asked to confirm that you want to save it. Save the configuration by clicking OK. The new interface will appear in the interface list that shows up in the next screen.
- If you want to activate the interface right away, click Activate. The screen should update the status of the interface to be active. However, `netcfg` might show the interface as active when it really isn't. This happens when you try to configure a nonexistent NIC. One of the easiest ways to check the interface is to run the `ifconfig interface name` command from the command line to see which interfaces are up and running.

You've just activated the new interface; now you need to set up a default gateway as follows:

- Click Routing to bring up the Network Configurator window, shown in Figure 7-9.
- Enter the default gateway IP address. The gateway device name should be the device you just configured.

![](img/f9ec99365f159bfe663f8ac29732663c_171_0.png)

- If you want to set up this device to forward IP packets to and from computers on your network, set the **Network Packet Forwarding (IPV4)** option.
- Save the new settings and quit the program.

You have configured the new interface and set up a default gateway. Test your new interface by pinging a computer on your network, using the `ping IP address` command. If you can ping a remote host, you have successfully configured the new interface.

To modify an existing network interface, do the following:

- Click **Interfaces**. Double-click the existing network interface line. Make changes as appropriate.
- After you make and save the changes, deactivate the interface first and then activate it.

### Caution

If you are using X Window System on a remote terminal to run the `netcfg` program, do not ever deactivate the interface being used to provide network connectivity to your terminal. If you deactivate the interface that is needed for your remote X connection, your X session will not work any longer and you will not be able to activate the interface without local access.

To delete an existing network interface, do the following:

- Click **Interfaces**. Select the existing network interface.
- Click **Delete** to complete the process. The statements in the preceding Caution apply here.

## Using a Default Gateway

Figure 7-10 shows two networks — network A (192.168.1.0) and network B (192.168.2.0).

![](img/f9ec99365f159bfe663f8ac29732663c_172_0.png)

![](img/f9ec99365f159bfe663f8ac29732663c_172_1.png)

Figure 7-10 Two distinct IP networks

These two networks are completely separate. The computers in either network can see the hosts in the same network just fine. A user using the 192.168.1.1 computer in network A can ping the other two computers by using the network interface IP addresses. However, that user can't access any of the host computers on network B, because no way exists for the packets in network A to go to network B. Because two distinct networks can be physically wired together, these two networks can be joined by using a gateway computer or a router, as shown in Figure 7-11.
