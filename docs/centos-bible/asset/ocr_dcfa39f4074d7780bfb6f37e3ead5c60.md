# # Setting Up Network Connections and LANs

The *interface* is the name of the wireless interface you want to change, such as `eth1` or `wlan0`. The *parameter* is the name of the option, and the *value* is replaced by its value. For example, to set your network name (ESSID) to `GalaxyBureau`, you could type the following as `root` user:

```
# iwconfig eth0 essid "GalaxyBureau"
```

Table 14-2 contains a list of available options for the `iwconfig` command. Refer back to the “Configuring the Wireless Interface” section for further details on these options.

The best place to add `iwconfig` options permanently in CentOS is the configuration file for your wireless interface in the `/etc/sysconfig/network-scripts` directory.

Options to `iwconfig` are added to the wireless interface file (such as `ifcfg-eth0` or `ifcfg-eth1`) using the `IWCONFIG` parameter. For example, to add an encryption-key value of `1234-1234-12` for your wireless LAN card, you could add the following line to your wireless-interface file:

```
IWCONFIG="key 1234-1234-12"
```

# # Understanding Internet Protocol Addresses

Whether you are using a wired or a wireless network, each computer you communicate with (including yours) must have a unique address on the network. In TCP/IP, each computer must be assigned an Internet Protocol (IP) address. This section gives you some background in IP addresses.

There are two basic ways to assign a hostname and an IP address to a network interface in Linux:

+   *   **Static Addresses** — With static IP addresses, each computer has an IP address that doesn’t change each time the computer reboots or restarts its network interface. Its IP address can be entered manually because it’s not assigned on-the-fly. You can do this at installation time or later using the Network Configuration window.

+   *   **Dynamic Addresses** — With dynamic addresses, a client computer gets its IP address assigned from a server on the network when the client boots. The most popular protocol for providing dynamic addresses is called the *Dynamic Host Configuration Protocol* (DHCP). With this method, a client computer may not have the same IP address each time it boots.

> If you expect to **add** and **remove** computers regularly from your LAN or if you have a **limited** number of IP addresses, you should use DHCP to assign IP addresses. Chapter 22 describes how to set up a DHCP server.