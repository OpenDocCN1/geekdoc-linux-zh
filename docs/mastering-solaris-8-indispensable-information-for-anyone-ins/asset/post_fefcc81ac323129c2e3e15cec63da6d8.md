
## The second method for capturing the output of snoop to a file is to use the -o option

![](img/256e02a6afce528d264a8d911fa0ff20_401_0.png)

```
% snoop -o <filename>
```

Here, <filename> is the path name of the file in which you want the output saved. Consider the following example:

```
% snoop -o /tmp/snoopy2
```

While the command is running, it will display the number of packets it is writing to the screen, as in the following example:

```
Using device /dev/be (promiscuous mode)
12
```

To terminate the capture of packets, press Ctrl+C. You can view the resulting file using the snoop command again but use the -i option this time. Direct the output of the command to a test file as in the following example:

```
% snoop -i /tmp/snoopy2>/tmp/snoopy2.txt
```

You can also capture just a certain part of a packet using the -x option. The syntax for the -x option is as follows:

```
% snoop <option> -x <offset>, <length>
```

In this example, <option> is either the -v or -V mode options and <offset> and <length> are the locations in bytes of where snoop should start and finish printing the contents of a particular packet. If you do not specify <length>, then snoop will print the contents of the entire packet from the start position. To display the entire packet, you can specify <offset> as 0 and leave off <length>, as in the following:

```
% snoop -x 0
```

The snoop utility has a powerful filtering feature that allows you to direct or deal with selective output for a single host, the source or destination host name, the network addresses, or the protocol type. The syntax for creating a filter is displayed in the following example:

```
% snoop <options> <expression>
```

<expression> is equal to any expression of a sort that can be recognized and acted upon by the snoop utility, as in % snoop -v macys reliant. This command will produce verbose-summary output for the two host systems.

Another type of filter that filters on the protocol type is % snoop <type>. <type> refers to the protocol parameter, for example, tcp, udp, or icmp. If you wanted to filter out all packets except TCP packets, you would use the following syntax: % snoop tcp. This command will give output on only TCP-based packets. The main snoop parameters are those that require additional arguments as described in Table 9.7.

### TABLE 9.7: PARAMETERS FOR THE SNOOP UTILITY

| Parameter | Output |
| --- | --- |
| from <host> | Packets coming from specified host. Argument <host> can be the system’s host name or IP address. |
| host <hostname> | Packets coming from or going to the specified host name; can also be the system’s IP address. |
| net <network> | Packets coming from or going to a network whose number is specified by <network>. |
| port <num> | Packets going to or coming from the TCP or UDP port number specified by <num>. |
| to <host> | Packets going to the specified host; argument <host> can be the system’s host name or IP address. |

## The `netstat` and `ifconfig` Utilities

The `netstat` command can display important network status information. In Solaris 8, the `netstat` command supports both IPv4 and IPv6. The `netstat` command can list information such as the following:

- The condition of DHCP as applied to your network interfaces (when used with the `-i` option)
- The state of your network interfaces
- Active sockets for protocols
- Kernel routing tables (when used with the `-r` and `-n` options) and multicast routing

The `ifconfig` command is used to display detailed information about your network interfaces. You can also use it to set or reset network interfaces. When the `/etc/rc2_d/S69inet` script runs at boot-up, it runs `ifconfig` to define each network interface as it comes up. You can use `ifconfig` to display and modify network interfaces. In its common form, `ifconfig -a`, a listing of active interfaces is shown. To display information about a particular interface, use the command `ifconfig <interface_name>`.

## The `nslookup` Utility

The `nslookup` utility is used to query the Internet domain name servers. When you give the utility a command, it will display the name and IP address of the default name server used by the system you are on. The following example shows the syntax:

```
$ nslookup

Default Server: reliant.mfield.com
Address: 168.168.99.01
```

You can perform a specific query using the nslookup utility. Give the set query command to get nslookup to display the mail exchanger (MX) record. If present, the MX record will specify a mail address for the domain. The following example demonstrates how to set the query:

```
> set query=MX
> reliant.mfield.com

reliant.mfield.com preference = 8, mail exchanger = barrie.mfield.com

reliant.mfield.com nameserver = barrie.mfield.com
```

You can establish different types of queries when using nslookup. If you set the query type to NS for name server, you will get three name server records. You must query a domain, however. If you query a host, the output will return start of authority (SOA) information, or you can use set query=any to get all of the information on that host.

## The whois Utility

Use the whois utility to look for a user on the Internet (i.e., an Internet directory entry that you specify). This utility will return site contact and registry information. You will be able to track the person responsible for a site. You can search by name or by handle. You can use the handle to narrow down the search. Even though the syntax used for names and handles by different servers will differ when you use whois, you can usually distinguish a handle from a name by preceding it with an exclamation mark, as in “!xxx”. You can then search for the handle.

The whois utility can also search on IP addresses. If you want to track someone who is sending spam mail, you can use whois to query the North American Internet Registry for the IP address on the header of the mail. The syntax is as follows:

```
$ whois -h whois.arin.net 195.168.xx.121
```

If the IP address is not found in the North American Internet Registry, the site will direct you to contact the European Registry for further information. You can go to the Web site and use whois there or you can use whois locally to get the information via the command line. Try the Web page at www.ripe.net/db/whois.html. It will give you a lot of useful information and will also direct you to IANA, the Internet Assignment Number Authority, which has codes for each country outside of the United States and Europe.

## File Transfer Utilities

Solaris provides utilities to transfer files over a network. You can use the rcp utility to transfer files between Unix or Solaris computers that are attached to a network. The rcp utility is similar to cp, and in like manner, you must specify the filename on the remote system or the system will use the original filename. The following example displays the syntax for using rcp to transfer a file:

```
% rcp doc.777 macsys:docs/docs.423
```

You can also use the ftp utility to transfer files between systems. The difference between rcp and ftp is that ftp is interactive and will let you browse through a directory on the remote system to identify files you may want to transfer. Here is the syntax for using ftp:

```
% ftp <hostname>
```

The remote system will prompt you for a login name and password. It will default to your login name for both systems if you press Return. If you have a different login or password, enter them at the prompt. You can also give a bin (binary) command so you can transfer both ASCII and binary files. The Solaris default is ASCII, so you can transfer only ASCII files in that mode successfully.

> **TIP** Because the Solaris default is ASCII, it is a good idea to get into the habit of using the bin command each time you transfer files using the ftp utility. It does not hurt ASCII files to transfer them in a binary format, but binary files are damaged by being transferred in ASCII format.

You can also use the ftp utility to connect to a remote site that has a distribution package of free software to download or transfer. Before downloading, determine where you are going to work. Most choose to work in the /var/tmp or /tmp directory. Log in as yourself and use cd to change to the /var/tmp directory. Then use ftp to connect to the host from which you want to download.
