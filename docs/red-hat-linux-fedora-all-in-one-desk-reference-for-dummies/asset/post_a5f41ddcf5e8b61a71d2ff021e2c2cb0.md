
## Chapter 4: Managing the Network

### In This Chapter

- Learning the TCP/IP configuration files
- Checking TCP/IP networks
- Configuring networks at boot time

Like almost everything else in Red Hat Linux, TCP/IP setup is a matter of preparing numerous configuration files (text files you can edit with any text editor). Most of these configuration files are in the /etc directory. The Red Hat installer helps by hiding the details of the TCP/IP configuration files. Nevertheless, it's better if you know the names of the files and their purposes so that you can edit the files manually, if necessary.

## Learning the TCP/IP Configuration Files

Running the Red Hat Network Configuration tool should be enough to get TCP/IP configured on your system. However, if you want to effectively manage the network, you should become familiar with the TCP/IP configuration files so you can edit the files, if necessary. (For example, if you want to check whether the name servers are specified correctly, you have to know about the /etc/resolv.conf file, which stores the IP addresses of name servers.)

Table 4-1 summarizes the basic TCP/IP configuration files. I describe these configuration files in the next few sections.

Table 4-1 Basic TCP/IP Network Configuration Files

| This File | Contains the Following |
|---|---|
| `/etc/hosts` | IP addresses and host names for your local network as well as any other systems you access often |
| `/etc/networks` | Names and IP addresses of networks |
| `/etc/host.conf` | Instructions on how to translate host names into IP addresses |
| `/etc/resolv.conf` | IP addresses of name servers |
| `/etc/hosts.allow` | Instructions on which systems can access Internet services on your system |
| `/etc/hosts.deny` | Instructions on which systems must be denied access to Internet services on your system |
| `/etc/nsswitch.conf` | Instructions on how to translate host names into IP addresses |

### /etc/hosts

The /etc/hosts text file contains a list of IP addresses and host names for your local network. In the absence of a name server, any network program on your system consults this file to determine the IP address that corresponds to a host name. Think of /etc/hosts as the local phone directory where you can look up the IP address (instead of a phone number) for a local host.

Here is the /etc/hosts file from a system, showing the IP addresses and names of other hosts on a typical LAN:

```
127.0.0.1          localhost          localhost.localdomain
# Other hosts on the LAN
192.168.0.100      lnbp933
192.168.0.50       lnbp600
192.168.0.200      lnbp200
192.168.0.233      lnbp233
192.168.0.40       lnbp400
```

As the example shows, each line in the file starts with an IP address, followed by the host name for that IP address. (You can have more than one host name for any given IP address.)

### /etc/networks

/etc/networks is another text file that contains the names and IP addresses of networks. These network names are commonly used in the routing command (/sbin/route) to specify a network by name instead of by its IP address.

Don't be alarmed if your Linux PC does not have the /etc/networks file. Your TCP/IP network works fine without this file. In fact, the Red Hat Linux installer does not create a /etc/networks file.

### /etc/host.conf

Red Hat Linux uses a special library (that is, a collection of computer code) called the resolver library to obtain the IP address that corresponds to a host name. The /etc/host.conf file specifies how names are resolved (that is, how the name gets converted to a numeric IP address). A typical /etc/host.conf file might contain the following lines:

```
order hosts, bind
multi on
```

The entries in the /etc/host.conf file tell the resolver library what services to use (and in which order) to resolve names.

The order option indicates the order of services. The sample entry tells the resolver library to first consult the /etc/hosts file, and then check the name server to resolve a name.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_362_0.png)

Use the multi option to indicate whether or not a host in the /etc/hosts file can have multiple IP addresses. Hosts that have more than one IP address are called multihomed because the presence of multiple IP addresses implies that the host has several network interfaces. (In effect, the host “lives” in several networks simultaneously.)

### /etc/resolv.conf

The /etc/resolv.conf file is another text file used by the resolver — the library that determines the IP address for a host name. Here is a sample /etc/resolv.conf file:

```
search mtgmry1.md.home.com
nameserver 164.109.1.3
nameserver 164.109.10.23
```

The first line tells the resolver how to search for a host name. For example, when trying to locate a host name myhost, the search directive in the example would cause the resolver to try myhost.mtgmry1.md.home.com first, then myhost.md.home.com, and finally myhost.home.com.

The nameserver line provides the IP addresses of name servers for your domain. If you have multiple name servers, you should list them on separate lines. They are queried in the order in which they appear in the file.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_362_1.png)

If you do not have a name server for your network, you can safely ignore this file. TCP/IP should still work, even though you may not be able to refer to hosts by name (other than those listed in the /etc/hosts file).

### /etc/hosts.allow

The /etc/hosts.allow file specifies which hosts are allowed to use the Internet services (such as TELNET and FTP) running on your system. This file is consulted before certain Internet services start. The services start only if the entries in the hosts.allow file imply that the requesting host is allowed to use the services.

The entries in /etc/hosts.allow are in the form of a servername:IP address format, where server refers to the name of the program providing a specific Internet service, and IP address identifies the host allowed to use that service. For example, if you want all hosts in your local network (which has the network address 192.168.0.0) to access the TELNET service (provided by the in.telnetd program), add the following line in the /etc/hosts.allow file:

```
in.telnetd:192.168.0.
```

If you want to let all local hosts have access to all Internet services, you can use the ALL keyword and rewrite the line as follows:

```
ALL:192.168.0.
```

Finally, to open all Internet services to all hosts, you can replace the IP address with ALL, as follows:

```
ALL:ALL
```

You can also use host names in place of IP addresses.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_363_0.png)

To learn the detailed syntax of the entries in the /etc/hosts.allow file, type man hosts.allow at the shell prompt in a terminal window.

### /etc/hosts.deny

This file is just the opposite of /etc/hosts.allow — whereas hosts.allow specifies which hosts may access Internet services (such as TELNET and TFTP) on your system, the hosts.deny file identifies the hosts that must be denied services. The /etc/hosts.deny file is consulted if there are no rules in the /etc/hosts.allow file that apply to the requesting host. Service is denied if the hosts.deny file has a rule that applies to the host.

The entries in /etc/hosts.deny file have the same format as those in the /etc/hosts.allow file — they are in the form of a server:IP address format, where server refers to the name of the program providing a specific Internet service and IP address identifies the host that must not be allowed to use that service.

If you have already set up entries in the `/etc/hosts.allow` file to allow access to specific hosts, you can place the following line in the `/etc/hosts.deny` file to deny all other hosts access to any service on your system:

```
ALL:ALL
```

To learn the detailed syntax of the entries in the `/etc/hosts.deny` file, type `man hosts.deny` at the shell prompt in a terminal window.

### /etc/nsswitch.conf

This file, known as the *name service switch* (NSS) file, specifies how services such as the name resolver library, NIS, NIS+, and local configuration files (such as `/etc/hosts` and `/etc/shadow`) interact.

NIS and NIS+ are *network information services* — another type of name-lookup service. Newer versions of the Linux kernel use the `/etc/nsswitch.conf` file to determine what takes precedence: a local configuration file, a service such as DNS (Domain Name Service), or NIS.

As an example, the following `hosts` entry in the `/etc/nsswitch.conf` file says that the resolver library should first try the `/etc/hosts` file, then try NIS+, and finally try DNS:

```
hosts:    files nisplus dns
```

You can learn more about the `/etc/nsswitch.conf` file by typing `info libc "Name Service Switch"` (including the quotes) in a terminal window.

## Checking Out TCP/IP Networks

After you configure Ethernet and TCP/IP (whether during Red Hat Linux installation or by running the Network Configuration tool later on), you should be able to use various networking applications without any problem. If you do run into trouble, Red Hat Linux includes several tools to help you monitor and diagnose problems.

### Checking the network interfaces

Use the `/sbin/ifconfig` command to view the currently configured network interfaces. The `ifconfig` command is used to configure a network interface (that is, to associate an IP address with a network device). If you run `ifconfig` without any command-line arguments, the command displays information about current network interfaces. The following is a typical invocation of `ifconfig` and the resulting output:
