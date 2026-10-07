
ypserv               0:off 1:off 2:off 3:off 4:off 5:off 6:off
autofs               0:off 1:off 2:off 3:off 4:off 5:off 6:off
dhcpd                0:off 1:off 2:off 3:off 4:off 5:off 6:off
mysqld               0:off 1:off 2:off 3:on 4:on 5:on 6:off
nscd                 0:off 1:off 2:off 3:off 4:off 5:off 6:off
ntpd                 0:off 1:off 2:off 3:off 4:off 5:off 6:off
squid                0:off 1:off 2:off 3:off 4:off 5:off 6:off
vmware               0:off 1:off 2:off 3:on 4:off 5:off 6:off
apcupsd              0:off 1:off 2:off 3:on 4:off 5:off 6:off
mysqld-skip          0:off 1:off 2:off 3:off 4:off 5:off 6:off
postgresql           0:off 1:off 2:off 3:off 4:off 5:off 6:off
vmware_old.0         0:off 1:off 2:off 3:off 4:off 5:off 6:off
iptables             0:off 1:off 2:on 3:on 4:on 5:on 6:off
isdn                 0:off 1:off 2:off 3:off 4:off 5:off 6:off
webmin               0:off 1:off 2:on 3:on 4:on 5:on 6:off
arkeia               0:off 1:off 2:off 3:off 4:off 5:off 6:off
xinetd based services:
    amanda:          off
    amidxtape:       off
    finger:          off
    linuxconf-web:   off
    rexec:           off
    rlogin:          off
    rsh:             off
    auth:            on
    telnet:          on
    tftp:            off
    wu-ftpd:         on
    talk:            off
    ntalk:           off
    pop-3:           on
    chargen:         off
    chargen-udp:     off
    daytime:         off
    daytime-udp:     off
    echo:            off
    echo-udp:        off
    time:            off
    time-udp:        off
    sgi_fam:         on
    amandaidx:       off

You can see from Listing 15.10 that there are many potential service vulnerabilities. As an example, look at the Telnet service. This should definitely not be on. There are many more secure services that accomplish the same mission; we use the secure shell (SSH). To turn off the Telnet service, issue the following chkconfig command:

```
chkconfig telnet off
```

Any service that you do not absolutely need, should be turned off. If you only need a service rarely, you might consider leaving it turned off until you need it and then turning it back off after use.

## TCP Wrappers

TCP Wrappers is a host-based security layer that applies to daemons started by the inetd daemon. The tcpd executable is a wrapper program that checks the /etc/hosts.allow and /etc/hosts.deny files to determine whether or not the specified service should be run. When tcpd is started by inetd, it reads the /etc/hosts.allow file and then /etc/hosts.deny. It grants or denies access based on the rules in these two files.

**Note** Red Hat and Mandrake have both switched to xinetd as a replacement for both inetd and TCP Wrappers. xinetd is discussed later in this chapter and in Chapter 12.

The /etc/hosts.allow file is a configuration file for the tcpd program. This file contains rules that describe which hosts are allowed to access which services on the localhost. The format is as follows:

```
service_list: host_list: [optional_command]
```

The service list is a comma-delimited list of service names to which this rule should be applied. The ftpd, telnetd, and httpd services are examples. The keyword ALL or ALL EXCEPT may be used as well. For instance, the following entry would allow all users to use all the local services except FTP:

```
ALL EXCEPT in.ftpd: ALL
```

The host list is a comma-delimited list of hostnames. The hostname may be represented as an IP address, a specific hostname, or a hostname that uses wildcard characters to make the match. If the hostname begins with a period, all hosts that share the string following that character will match this rule. For example, the line below would match any attempt to Telnet in from a computer on the somedomain.com network.

```
in.telnetd: somedomain.com
```

If a numeric IP is used, it may be a full IP address for a specific machine or may consist of only the partial address consisting of period-delimited numbers, causing any IP that starts with those numbers to be matched. The host list may contain these keywords: ALL, LOCAL, PARANOID, and EXCEPT. The ALL keyword would cause all hosts to match. The LOCAL keyword causes any local login to match. The PARANOID keyword means that any host whose name is being spoofed will match. The EXCEPT keyword is most often used in conjunction with ALL as in this example:

```
ALL EXCEPT hostname
```

This would match every host except the one that is listed. Another variation on this theme allows for the rule to include an expression in the form:

```
12.34.56.0/255.255.254.0
```

This will be interpreted as a net/mask pair and will be matched if the net portion is equal to the bitwise and of the address and the mask portion. Thus it would allow any address between 12.34.56.0 and 12.34.57.255 access to the system.

The *optional_command* argument identifies a command to be run every time the rule is matched. For example, this might be used to send e-mail to the superuser when a certain host uses the Telnet service. There are a number of expansions that may be used; they are covered in the hosts.allow man page. Table 15.2 shows example entries from /etc/hosts.allow and what they mean.

### Table 15.2: Sample /etc/hosts.allow Entries

| Line | Meaning |
| --- | --- |
| in.ftpd:ALL EXCEPT 123.45.67. | FTP service is allowed to all except those on the 123.45.67.* domain. |
| ALL:ALL | All services are allowed to all hosts. |
| ALL: 123.45.67.89 | All services are allowed to the 123.45.67.89 host. |
| pop3d:LOCAL | The POP3 service is allowed to all local accounts. |
| in.talkd:host.somedomain.com, host2.somedomain.com | The Talk service is allowed to both host and host2 in somedomain.com. |
| in.telnetd:somedomain.com | The Telnet service is allowed to any host on the somedomain.com domain. |

The /etc/hosts.deny file uses the same format as /etc/hosts.allow but serves the opposite purpose. Lines in this file determine which hosts will be denied access to the specified service. The /etc/hosts.allow and /etc/hosts.deny files work in conjunction. If the /etc/hosts.allow file listed the rule ALL:ALL, allowing open access to all services, but the /etc/hosts.deny file included lines that prohibited some hosts from using some services, /etc/hosts.deny would override the open access for only the hosts and services specified. The deny file is the dominant file. An open system would include the ALL:ALL entry in the /etc/hosts.allow file and nothing in the /etc/hosts.deny file, granting access to everyone and denying it to no one. A completely closed system would have nothing in /etc/hosts.allow and ALL:ALL in /etc/hosts.deny, thereby denying access to everyone.

The TCP Wrappers package includes two tools you can use to check your TCP security. There is tcpdchk, which examines the /etc/inetd.conf, /etc/hosts.allow, and /etc/hosts.deny files for blatant errors. To display a list of all access rules, use the following command:

```
# tcpdchk -v
```

The command will return a list of accesses explicitly permitted or denied, including the daemon to which the access pertains, the client to whom the access pertains, and the actual access determination. Here is an example:

```
>>> Rule /etc/hosts.allow line 18:
daemons:   in.telnetd
clients:   .ntnet.net
access:    granted
```

The other tool is the tcpdmatch utility, which allows you to test for a specific daemon and client. The command looks like this:

```
# tcpdmatch in.telnetd www.macroschaft.com
```

The command will return the following if access is granted:

```
client:  hostname www.macroschaft.com
client:  address 117.4.137.45
server:  process in.telnetd
access:  granted
```

If the host is denied access, the response will look like this:

```
client:  hostname www.macroschaft.com
client:  address 117.4.137.45
server:  process in.telnetd
matched: /etc/hosts.deny line 10
access:  denied
```
