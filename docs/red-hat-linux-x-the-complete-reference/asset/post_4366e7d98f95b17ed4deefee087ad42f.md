
Table 38-8: Resolver Options, host.conf

| Options | Description |
|---|---|
| alert | Checks addresses of remote sites attempting to access your system; you turn it on or off with the on and off options |
| nospoof | Confirms addresses of remote sites attempting to access your system |
| trim | Checks your local host's file; removes the domain name and checks only for the hostname; enables you to use only a hostname in your host file for an IP address |
| multi | Checks your local hosts file; allows a host to have several IP addresses; you turn it on or off with the on and off options |

In the next example of a host.conf file, the order option instructs your resolver first to look up names in your local /etc/hosts file, and then, if that fails, to query domain name servers. The system does not have multiple addresses.

## /etc/host.conf

```
# host.conf file
# Lookup names in host file and then check DNS
order bind host
# There are no multiple addresses
multi off
```

## /etc/nsswitch.conf: Name Service Switch

Different functions in the standard C Library must be configured to operate on your Linux system. Previously, database-like services, such as password support and name services like NIS or DNS, directly accessed these functions, using a fixed search order. For GNU C Library 2.x, used on current versions of Linux, this configuration is carried out by a scheme called the Name Service Switch (NSS), which is based on the method of the same name used by Sun Microsystems Solaris 2 OS. The database sources and their lookup order are listed in the /etc/nsswitch.conf file.

The /etc/nsswitch.conf file holds entries for the different configuration files that can be controlled by NSS. The system configuration files that NSS supports are listed in Table 38-9. An entry consists of two fields: the service and the configuration specification. The service is followed by a colon. The second field is the configuration specification for that file, which holds instructions on how the lookup procedure will work. The configuration specification can contain service specifications and action items. Service specifications are the services to search. Currently, valid service specifications are nis, nis-plus, files, db, dns, and compat (see Table 38-10). Not all are valid for each configuration file. For example, the dns service is valid only for the hosts file, whereas nis is valid for all files. The following example will first check the local /etc/password file and then NIS.

```
passwd: files nisplus
```

Table 38-9: NSS Supported Files

| Files | Description |
|---|---|
| aliases | Mail aliases, used by Sendmail |
| ethers | Ethernet numbers |
| group | Groups of users |
| hosts | Hostnames and numbers |
| netgroup | Network-wide list of hosts and users, used for access rules; C libraries before glibc 2.1 only support netgroups over NIS |
| network | Network names and numbers |
| passwd | User passwords |
| protocols | Network protocols |
| publickey | Public and secret keys for SecureRPC used by NFS and NIS+ |
| rpc | Remote procedure call names and numbers |
| services | Network services |
| shadow | Shadow user passwords |

Table 38-10: NSS Configuration Services

| Service | Description |
|---|---|
| files | Checks corresponding /etc file for the configuration (for example, /etc/hosts for hosts); this service is valid for all files |
| db | Checks corresponding /var/db databases for the configuration; valid for all files except netgroup |
| compat | Valid only for passwd, group, and shadow files |
| dns | Checks the DNS service; valid only for hosts file |
| nis | Checks the NIS service; valid for all files |
| nisplus | NIS version 3 |
| hesiod | Uses Hesiod for lookup |

An action item specifies the action to take for a specific service. An action item is placed within brackets after a service. A configuration specification can list several services, each with its own action item. In the following example, the entry for the network file has a configuration specification that says to check the NIS service and, if not found, to check the /etc/protocols file:

```
protocols: nisplus [NOTFOUND=return] files
```

An action item consists of a status and an action. The status holds a possible result of a service lookup, and the action is the action to take if the status is true. Currently, the possible status values are SUCCESS, NOTFOUND, UNAVAIL, and TRYAGAIN (service temporarily unavailable). The possible actions are return and continue: return stops the lookup process for the configuration file, whereas continue continues on to the next listed service. In the preceding example, if the record is not found in NIS, the lookup process ends.

Shown here is a copy of the current Red Hat /etc/nsswitch.conf file, which lists commonly used entries. Comments and commented-out entries begin with a # sign.

/etc/nsswitch.conf

```
#
# /etc/nsswitch.conf
#
# An example Name Service Switch config file.
passwd:      files nisplus
shadow:      files nisplus
group:       files nisplus
hosts:       files nisplus dns
bootparams:  nisplus [NOTFOUND=return] files
ethers:      files
netmasks:    files
networks:    files
protocols:   files
rpc:         files
services:    files
netgroup:    nisplus
publickey:   nisplus
automount:   files nisplus
aliases:     files nisplus
```

## Network Interfaces and Routes: ifconfig and route

Your connection to a network is made by your system through a particular hardware interface, such as an Ethernet card or a modem. Data passing through this interface is then routed to your network. The ifconfig command configures your network interfaces, and the route command sets up network connections accordingly. If you configure an interface with a network configuration tool, such as redhat-config-network, you needn't use ifconfig or route. However, you can directly configure interfaces using ifconfig and route, if you want. Every time you start your system, the network interfaces and their routes must be established. This is done automatically for you when you boot up by ifconfig and route commands executed for each interface by the /etc/rc.d/init.d/network initialization file, which is executed whenever you start your system. If you are manually adding your own interfaces, you must set up the network script to perform the ifconfig and route operations for your new interfaces.

## Network Startup Script: /etc/rc.d/init.d/network

On Red Hat, your network interface is started up using the network script in the /etc/rc.d/init.d directory. This script will activate your network interface cards (NICs) as well as implement configuration information such as gateway, host, and name server identities. You can manually shut down and start your network interface using this script and the restart, start, or stop options. You can run the script on Red Hat with the service command. The following commands shut down and then start up your network interface:

```
service network stop
service network start
```

If you are changing network configuration, you will have to restart your network interface for the changes to take effect:

```
service network restart
```

To test if your interface is working, use the ping command with an IP address of a system on your network, such as your gateway machine. The ping command continually repeats until you stop it with a CTRL-C.

```
ping 192.168.0.1
```

## Interface Configuration Scripts: /etc/sysconfig/network-scripts

The /etc/rc.d/init.d/network file performs the startup operations by executing several specialized scripts located in the /etc/sysconfig/network-scripts directory. The network script uses a script in that directory called ifup to activate a network connection, and ifdown to shut it down. ifup and ifdown will invoke other scripts tailored to the kind of device being worked on, such as ifup-ppp for modems using the PPP protocol, or ifup-ipv6 for network devices that use IP Protocol version 6 addressing.

Note You can activate and deactivate network interfaces using the Network Device Control tool accessible from the System Tools menu.
