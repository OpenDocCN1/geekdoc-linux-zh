
## Configuring Linux for a Local Network

### Configuring Hostnames

The hostnames described earlier (in “Resolving Hostnames”) are configured in a couple of ways:

- **On DNS** Your network administrator should be able to add an entry for your system to your network’s DNS server. This entry should make your computer addressable by name from other computers on your local network, and perhaps from the Internet at large. Alternatively, remote systems’ /etc/hosts files can be modified to include your system.

- **On your local computer** Various local programs should know your computer’s name. For instance, you may want to have your hostname displayed as part of a command prompt or entered automatically in e-mail programs. For this task, you must set your hostname locally. Note that this is entirely independent of your DNS hostname. In theory, you can set the two to very different values, but this practice is likely to lead to confusion and perhaps even failure of some programs to operate properly.

The most basic tool for setting your hostname locally is called, appropriately enough, **hostname**. Type the command alone to see what your hostname is, or type it with a new name to set the system’s hostname to that name:

```
hostname nessus.example.com
```

Similar commands, **domainname** and **dnsdomainname**, display or set the computer’s domain name (such as example.com). The **domainname** command sets the domain name as used by Network Information System (NIS), whereas **dnsdomainname** sets the domain name as used by DNS. These commands don’t affect remote servers—just the name given to programs that use calls designed for these servers.

Many Linux distributions look in the /etc/hostname or /etc/HOSTNAME file for a hostname to set at boot time. Thus, if you want to set your hostname permanently, you should look for these files, and if one is present, you should edit it. Fedora uses /etc/sysconfig/network for this purpose, among others. If you can’t find one of these files, consult your distribution’s documentation; it’s conceivable that your distribution stores its hostname in some unusual location.

In Exercise 8.1, you’ll familiarize yourself with some of the tools used to configure basic network settings. You’ll use these tools both to study and to change your network configuration.

### EXERCISE 8.1: Configuring a Network Connection

In this exercise, the assumption is that the computer is correctly configured to use an IPv4 Ethernet network, including both local network access and access to a larger network (probably the Internet) via a router.

Some of the procedures in this exercise can easily break your network connectivity if something goes wrong. If this happens, typing **ifdown** followed by **ifup** is one way to recover. If this fails, rebooting the computer is almost certain to work, although it’s a radical solution.

To study and modify your system's network configuration, follow these steps:

1. Log into the Linux system as a normal user.
2. Launch an xterm from the desktop environment's menu system, if you used a GUI login method.
3. Acquire root privileges. You can do this by typing `su` in an xterm, by selecting Session > New Root Console from a Konsole, or by using `sudo` (if it's configured) to run the commands in the following steps.
4. Type `ifconfig`. This command displays information about your local network settings for all your network interfaces. Most systems have both a loopback interface (`lo`) and an Ethernet interface (`eth0`). Look for a line in the Ethernet section that includes the string `inet addr:`. The following 4-byte number is your IP address. Write it down, as well as the value of your netmask (`Mask:`). Study the other information in this output, too, such as the number of received (RX) and transmitted (TX) packets, the number of errors, the number of collisions, and the Ethernet adapter's hardware address.
5. Type `route -n`. The output is your computer's routing table information. This normally includes information about the loopback network address (`127.0.0.0/24`), the local network address, and a default route (identified as the route for `0.0.0.0`). Some systems may display fewer or additional lines, depending on local configuration. The default route includes an IP address under the Gateway column. Write down that address.
6. Use `ping` to test connectivity to both local and remote computers. (This command is described in more detail shortly, in “Testing Basic Connectivity.”) You need the name or IP address of at least one local computer and at least one distant computer (beyond your local router). Type `ping address`, where `address` is the name or IP address of each test machine. Perform this test for `localhost` or `127.0.0.1`, your own machine (use the IP address you noted in step 4), your local router (use the IP address you noted in step 5), and a distant computer (if you're connected to the Internet, you can use an Internet-accessible site, such as `www.linux.org`). All of these `ping` tests should be successful. Note, however, that some systems are configured to ignore packets sent by `ping`. Thus, some of these tests may fail if you run into such systems. You can learn the configuration of local systems from their administrators, but for Internet sites, you may want to simply try another site if the first one you test fails.
7. Bring down the local Ethernet connection by typing `ifconfig eth0 down`.
8. Repeat steps 4–6. Note that the `eth0` interface is no longer shown when you type `ifconfig`, all routes associated with it have been removed from the routing table, and `pinging` systems accessible from the interface no longer works. (Linux retains some information about its former Ethernet link, so you may still be able to `ping` the computer itself via its former `eth0` address.)
9. Bring the local Ethernet connection back up by typing `ifconfig eth0 up address netmask mask`, where *address* is the original IP address and *mask* is the original netmask, both as identified in step 4.
10. Repeat steps 4–6. Note that the `ifconfig` command automatically added back your local network to the routing table but that the default route is still missing. As a result, you can't contact any systems that are located off the local network. If your DNS server is such a system, this means your ability to contact even local machines by name may be impaired as well.
11. Restore the default route by typing `route add default gw gateway`, where *gateway* is the router address you identified in step 5.
12. Repeat steps 4–6. If your network configuration is typical, all connectivity should be restored. (Some more exotic systems may still be lacking certain routes.)

![](img/f339a9f48c4b443e61c74acb4c9c3da4_470_0.png)

## Using PPP with DSL

Broadband users, and particularly those with Digital Subscriber Line (DSL) connections, sometimes have to use a variant of PPP to make their connections. PPP is a login-based way to access the Internet—you use a PPP utility to initiate a connection to a remote computer, which includes an exchange of a username and a password. A decade ago, PPP was used in dial-up Internet access (and it’s still used in this capacity), but some DSL providers have adapted PPP for their own purposes. In the case of DSL, this configuration method is called PPP over Ethernet (PPPoE).

In many cases, the simplest way to use a PPPoE configuration is to purchase a broadband router. This device attaches to the DSL modem and makes the PPPoE connection. The broadband router then works just like an ordinary Ethernet or Wi-Fi router, as far as your local computers are concerned, so you can configure Linux as you would on any other local network.

If you must connect a Linux system directly to a DSL network that uses PPPoE, you must use a Linux PPPoE client. Most Linux distributions ship with such clients; but configuration details vary from one distribution to another. Your best bet is to look for your distribution’s GUI network configuration tool; chances are, you’ll be able to find a set of options that are clearly labeled as applying to DSL or PPPoE.
