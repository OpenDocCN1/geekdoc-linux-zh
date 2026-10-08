
All other DHCP servers provide similar/restart configuration scripts—if you installed another DHCP server, check its control files in /etc/init.d for the name of the script that you need to execute and any additional arguments that you may need to supply.

## Specifying Additional DHCP Server Configuration File Entries

In addition to the DHCP configuration statements discussed in the previous section, you can specify several other options in your DHCP server's configuration file. Using these other options can provide your DHCP server with additional configuration information, which enables it to forward this information to any of its clients.

Additional global dhcpd.conf statements that you may find useful are the following. An example of a dhcpd.conf file that uses these statements is given following the list, to clear the context in which each statement is used:

- default-lease-time: This DHCP server configuration option enables you to specify the default period of time for which a lease will be valid. The time period is specified as an integer of seconds.

- ddns-update-style: This declaration is used if your site uses a DNS (Domain Name Server) that can be automatically updated as addresses are assigned by the DHCP server and you installed the autodns-package on your DHCP server to integrate the two. If your site does not use a DNS server that accepts updates from a DHCP server, you should set this parameter to None to avoid potential performance problems.

- ip-forwarding: If, for example, you don't want a DHCP client to be able to forward IP requests to other networks, you may want to set this parameter to off. This option is used sometimes on local-only IP networks.

- max-lease-time: This DHCP server configuration option enables you to specify the maximum period of time for which a lease will be valid. The time period is specified as an integer of seconds.

You can use DHCP to provide specific IP addresses to hosts within a subnet group, where a host is identified by MAC address. This is done using the host declaration within a subnet group. An example of this, an associated, host-specific command, is the following:

```
authoritative;
option domain-name "vonhagen.org";
option domain-name-servers 192.168.6.1, 208.272.222;
option ddns-update-style interim;
option default-lease-time 28800;
option max-lease-time 86400;
option ip-forwarding off;
subnet 192.168.6.0 netmask 255.255.255.0 {
range 192.168.6.160 192.168.6.190
```

```
host dorothy (
    hardware ethernet 00:1E:0C:1D:75:1D;
    fixed_address 192.168.6.69;
    option host_name "dorothy"
)
```

Note that the example for the specific host named dorothy overrides any default values earlier in the file.

## Picking the Right Lease Period

The lease time for your server's DHCP clients is a delicate balance between usability and serviceability. You want clients that have been configured via DHCP to keep that configuration as long as they need that information, but you also want to maximize the availability of DHCP configuration to other clients on your network. This is especially (and primarily) important on networks where the number of users exceeds the number of available IP addresses.

Identifying conceivable patterns in how users access and use your DHCP server will help determine a usable lease period. For example, if you know that the number of clients exceeds the number of available IP addresses, it's in your best interest to keep the lease period as short as possible. On the other hand, you want to minimize traffic and the load on your DHCP server. If you have more users than IP addresses and mobile users frequently connect to your network, you will want to keep the lease time as short as possible. However, if systems typically appear on your network for a certain period of time (30 minutes, an hour, etc.), you will want to set the lease time to minimize lease requests.

Another consideration is the amount of time required to recover from network problems or hardware failures on the DHCP server. For example, if your DHCP server were to crash and been, the lease period would define the maximum amount of time that clients would maintain their current configuration.

Finally, consider the silly user factor. If clients of your DHCP server are setting up network services that they expect to access for a significant amount of time, you may need to make sure that your DHCP leases are valid for at least that period of time. Even though DHCP leases are supposed to be renewed when they are in use, this might not happen for one reason or another. As we all learned in Cub Stocks, Browns, or similar groups, "Be prepared." If users report problems, you can always fix things and report a success story, but sometimes no comments are the best comments of all.

## Managing a DHCP Server Graphically

As you might expect, the Ubuntu repository provides an excellent GTK utility for graphically configuring a DHCP server. If you have installed this package (admin-dhcpd) as part of the instructions for installing a DHCP server in the section of this chapter entitled "Installing a DHCP Server."

Installing the gadmin-dhcpd package creates a GADMIN-DHCP entry on the Applications System Tools menu, which you can select to start Ubuntu's graphical DHCP server configuration tool. Unfortunately, the first time you use this utility, you'll need to specify the location of the DHCP server configuration.

# Part III: Ubuntu System Administrators
