
There will then be a series of lines to specify the primary and secondary servers in the domain, along with a cache statement.

```
:
:             domain              file
cache .                     named.ca
primary mydomain.com        named.hosts
primary 0.0.127.in-addr.arpa named.local
primary 10.100.100.in-addr.arpa named.rev
secondary my2dom.com        192.168.10.6 named.hosts
```

The version of BIND from 8 onward will have the same information but in a slightly different format. A sample listing showing how a primary or master nameserver is set up in the later version is shown below, which is in the named.conf file (normally in /etc or /etc/named.d):

```
zone "mydomain.com" IN {
    type master;
    file "mydomain.com.zone";
    allow-update {none;};
};
```

With the later version, there is a control utility called rndc, which allows you to administer the named daemon. The configuration file for rndc is /etc/rndc.conf, and, additionally, you need to specify authentication keys in both /etc/rndc.conf and /etc/named.conf, which must match. You will need to generate HMAC-MD5 keys for both configuration files using the following command:

```
dsnssec-keygen -a hmac-md5 -b <bit-length> -n HOST <key-file-name>
```

The default used by rndc to connect to is 953. Once the command is set up, the rndc command can be used with the following options shown in Table 9.1.

### Table 9.1 rndc Options

| Option | Description |
| :--- | :--- |
| `halt` | Stops named daemon immediately |
| `refresh` | Refreshes the database |
| `Reload` | Reloads the zone files but keep the cached files |
| `Stop` | Stops the service gracefully |

## EXERCISE 9.1: Making a Name Server Authoritative

In this exercise, you will learn how to make a secondary name server authoritative for a domain for a server running Bind 9 as you are about to decommission the existing primary name server.

- In the `named.conf` file on the secondary server, check to see whether it is designated as the secondary for the zone you are interested in.
- Change `type secondary` to `type master`.
- Change the `allow update` option to `none`.
- Power down the master server and then reboot the server you have just changed to master.
- This new server should now be authoritative for this domain.

## Network Time Protocol

NTP is the defined protocol for synchronizing clocks of computer systems over a network, including the Internet. There are many time servers located across the world, and the source can be an atomic clock or via a satellite receiver. The accuracy that is obtained is very good and is typically no more than a few milliseconds. Like DNS servers, there is a hierarchy with primary or Stratum 1 timeservers and secondary or Stratum 2 servers. Those servers at a lower level always synchronize themselves to a server at a higher level. There are a number of public timeservers available, and those operated by the National Institute of Science and Technology (NIST) and US Naval Observatory (USNO) within the United States are particularly reliable.

Within the Linux system, there is an NTP client which is implemented as a continuously running daemon process. This process runs in the kernel space due to the sensitivity of timing.

The main configuration file for NTP is /etc/ntp.conf, and the servers you will synchronize to, as well as what networks are allowed to synchronize to your server, are described. You need to define a number of servers to synchronize to ensure there is redundancy in case of network or server failures. To specify a pair of servers to synchronize to, the ntp.conf will need to be modified as such:

```
server lerc-dns.lerc.nasa.gov # Stratum 1 server
server ntp.time.edu           # Stratum 2 server
```

You must then restrict the access that you allow these time servers; for instance, you do not want them to query your NTP server.

```
restrict lerc-dns.lerc.nasa.gov mask 255.255.255.255
nomodify noall no trap noquery
restrict ntp.time.edu mask 255.255.255.255 nomodify
notrap noquery
```

Using the same command, you can allow hosts on your local network to query your time servers.

```
restrict 10.10.10.0 mask 255.255.255.0 nomodify
notrap
restrict 127.0.0.1
```

The use of the restrict command can seem to be confusing; but it should be thought of as everyone being allowed to query your server, and you are just reducing this overall access. Also note that in the code above, the local host (127.0.0.1) is allowed full access. You need to ensure that ntpd is started on boot with the chkconfig command, and also start the service manually for this first time with the service command.

```
chkconfig ntpd on
service ntpd start
```

To find and use an NTP server easily, there is a pool of servers that you can use. These NTP pools contain hundreds of public NTP servers that their operators allow to be used for time synchronization. You will need to define the pool you want to use with the DNS name region.pool.ntp.org, where you substitute region for the country or state where you live. More information can be found at www.pool.ntp.org. The utility program ntpq can be used to monitor the NTP daemon to determine the performance. The command uses standard NTP mode in six control message formats. This command is useful to see what time servers are currently being polled using ntpq -p.

In older versions of ntp, the local date and time can be set using ntpdate. This functionality is now in ntpd, but the older version is still in use. The command can be run manually, or usually it is run automatically at boot time.

## date Command

The date command can be used to display or set the date on a system that does not have an NTP server installed. The options for the command are shown in Table 9.2, date options.

### Table 9.2 date options

| Option | Description |
| :--- | :--- |
| -a | Adjust the date when the time has drifted. |
| -u | Display or set the time in GMT |
| -s datetime | Set the time and date |

## Windows Interoperability

There are numerous Microsoft Windows workstations and servers in use today, and interoperability with Linux is normally an essential task any system administrator needs to undertake. There are a number of utilities to allow file sharing between systems, with the most common utility being *Samba*. Samba provides file and print services to all Server Message Block/Common Internet File System (SMB/CIFS) clients, which includes most versions of Microsoft Windows operating systems as well as Linux/UNIX servers and clients.

> **Note**  
> SMB is an application layer network protocol, and is used as a shared-access protocol between different machines on a network. Microsoft modified the original specification for SMB and produced the CIFS, which was implemented in their products until Microsoft Vista was launched (which uses SMB 2.0).

## Remote Desktop

With any mixed environment, you may need to manage both Linux and Microsoft *Windows* clients and servers. Natively within Microsoft Windows, there is a remote desktop application that uses the Remote Desktop Protocol (RDP). Within Linux, the open-source product `rdesktop` can be used to present the target desktop. This is based on the X-Windows system. To connect to a remote host http://hostname.myccorp.com with IP address 10.10.100.23, either of the following commands can be used:

```
rdesktop hostname.myccorp.com
rdesktop 10.10.100.23
```

> **Note**  
> The target server or client must have the remote desktop connection enabled for this to work. In addition, you may need to supply user name and password credentials applicable to the target host. The protocol runs on port 3389, which will need to be open on any intermediate firewalls.

## Virtual Network Computing

VNC was developed by AT&T to administer machines. This is a client-server application, and there are now a number of different versions that are both open source and commercial. The VNC server itself is often built into the
