
# DHCP Configuration

```
host emailserver { option host-name "test.linux4biz.net"; hardware ethernet 00-20-18-8B-3F-9E; fixed-address 192.168.0.10; }
```

Here, the first line defines the declaration for a single computer: `host` is a configuration option, and `emailserver` is a reference name for the computer that will be allocated a static IP address. You can use any reference name here, and we usually use a name that reflects the purpose of the machine in question.

The second line specifies the hostname of the machine (`test.linux4biz.net`), and the third line defines the Ethernet hardware address.

You can find the Ethernet hardware address of a Linux machine by executing the following command on that machine:

```
$ /sbin/ifconfig
```

Check the first line of output; it should look something like this:

```
eth0 Link encap:Ethernet HWaddr 00:D0:B7:0A:E7:41
```

You can find the Ethernet hardware address on a Windows machine by executing this command at the command prompt:

```
> ipconfig /all
```

In this case, search for the line that starts with the string **Physical Address**, under your Ethernet card description:

```
Physical Address . . . . . . . . : 00-20-18-8B-3F-9E
```

The fourth line defines the static IP address to be assigned to the server whose hardware Ethernet address matches the one given.

It is recommended that you back up the `/etc/dhcpd.conf` file when you’ve finished your initial configuration, and keep it safe – just in case it gets corrupted or changed accidentally.

## Installing and Configuring a DHCP Client

We’ve talked about how to configure the DHCP server, but what about the DHCP client? In fact, there is a default DHCP client software installed on all Red Hat Linux 9 installations, and if you’ve configured your Linux machine to be a DHCP client, then it’s using that DHCP client program now.

If you want to configure a Linux machine to be a DHCP client, then you can set this configuration either at installation or subsequently via the Network Configuration tool. To launch the Network Configuration tool, select **Main Menu | System Settings | Network** or type the following command at the command line:

```
$ redhat-config-network
```

Under the **Devices** tab, select the Ethernet device and click on **Edit**. Make sure the **Activate device when computer starts** option is enabled, and select the **Automatically obtain IP address settings with dhcp** option:

![](img/b852150740856958b10aff9e8c9d2adc_408_0.png)

Click on **OK** when you're finished, then on **Apply** to apply the changes. The changes will take effect from the next reboot.

## Configuring a Windows 2000 Machine to Use a DHCP Server

If you've got a Windows 2000 machine (for example, a Win2K laptop that you use both at home and at work), here's how to configure it to get its network settings from a DHCP server:

1. Click on **Start | Settings | Control Panel** to open the Control Panel window.
2. Double-click on **Network and Dial-up Connections** and then on **Local Area Connection**.
3. Click the **Properties** button. In the resulting **Local Area Connection Properties** dialog, highlight **Internet Protocol (TCP/IP)** and click on **Properties**.
4. In the resulting **Internet Protocol (TCP/IP) Properties** dialog, select **Obtain an IP Address automatically** and **Obtain DNS server address automatically**.
5. Click on **OK** to confirm the changes, and then on **OK** again to implement the changes. At this point, the DHCP client program will try to get address information from the DHCP server.

If you like, you can check the new IP address allocated by the DHCP server by executing the `ipconfig /all` command on the command prompt:

```
C:\>ipconfig /all
Windows 2000 IP Configuration
   Host Name . . . . . . . . . . . : my-win2k-laptop
   Primary DNS Suffix . . . . . . : 
   Node Type . . . . . . . . . . . : Hybrid
   IP Routing Enabled. . . . . . . : No
   WINS Proxy Enabled. . . . . . . : No
   DNS Suffix Search List. . . . : linux4biz.net

Ethernet adapter Local Area Connection:
   Connection-specific DNS Suffix : linux4biz.net
   Description . . . . . . . . . . . : Xircom CreditCard Ethernet 10/100 + Modem
   Physical Address. . . . . . . . : 00-80-C7-8B-C2-E3
   DHCP Enabled. . . . . . . . . . : Yes
   Autoconfiguration Enabled . . : Yes
   IP Address. . . . . . . . . . . : 192.168.0.129
   Subnet Mask . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . : 192.168.0.1
   DHCP Server . . . . . . . . . : 192.168.0.99
   DNS Servers . . . . . . . . . : 192.168.0.1
   Lease Obtained. . . . . . . . . : 19 February 2003 09:01:21
   Lease Expires . . . . . . . . . : 22 February 2003 09:01:21
```

This allows you to see the TCP/IP information that the Windows DHCP client has acquired from the DHCP server. In the above output, the **DHCP Enabled** property is set to **Yes**, indicating that the Windows client machine is configured to get IP information from a DHCP server. The physical address of this machine (its MAC address, taken from its Ethernet card) is `00-80-C7-8B-C2-E3`; the DHCP server has leased the IP address `192.168.0.129` to the machine, and the lease will expire three days from when it was obtained.

## Summary

We've covered six common services in this chapter. It's unlikely that you'll need them all in a home environment, and it's certainly unlikely that you'll ever install all of these services onto a single machine, except to experiment with them! Most medium-size office environments will have at least some of these services, and in a production situation you would often assign at least one dedicated machine to any of these services.

There are so many configuration options for all these services that we can't possibly cover them all here. There is a mass of useful information on the web, both in formal documentation and on newsgroups, and you have the man pages too. Here are just a few sites that provide more documentation and developments on some of the services here:

- www.sendmail.org – the official sendmail web site
- www.redhat.com – the official site for Red Hat Linux
- www.samba.org – the official web site for SAMBA
- http://www.rfc-editor.org – a searchable Collection of all RFCs
- http://www.isc.org/products/DHCP/ – the official site for DHCP
- http://www.tldp.org/ – the Linux documentation Project site
- http://www.linux4biz.net/writing.htm – contains useful articles on Linux
- http://www.linuxsecurity.com/ – a security news site for Linux

In the next chapter we will delve further into the realms of systems administration, by looking at system configuration, logs, backups and archives, and a closer look at the Linux kernel.

# Chapter 10
## Advanced System Administration

We have dealt exclusively with the Personal Desktop version of Red Hat Linux in this book, but we still need to perform a number of administrative tasks to keep our system running well; system administration is not limited to full multi-user servers. We have already discussed how to install the operating system and how to use it for day-to-day operations. So, our next goal is to discuss some of the more advanced administrative aspects of managing a Linux system. More specifically, we will focus on the following tasks in this chapter:

- Examining important configuration files and the information they contain
- Analyzing system log files to track problems
- Backing up and archiving
- Installing new applications from source code
- Building and customizing the Linux kernel

By understanding the rationale for performing these tasks, as well as how to actually implement them, we will get a better feel for how the operating system works and how to manage it properly. As you will see, Linux provides us with the ability to control and administer nearly all aspects of its operation, including the core part of the system, the kernel.

We will start by looking at the system configuration, including how to find the information we need and then to modify it to suit our requirements.
