
## squid — (Version 2.2.DEvel3, 1,861K)

Squid is a high-performance proxy caching server for web clients, supporting FTP, gopher, and HTTP data objects. Unlike traditional caching software, Squid handles all requests in a single, non-blocking, I/O-driven process. Squid keeps meta data and especially hot objects cached in RAM, caches DNS lookups, supports non-blocking DNS lookups, and implements negative caching of failed requests. Squid supports SSL, extensive access controls, and full request logging. By using the lightweight Internet Cache Protocol, Squid caches can be arranged in a hierarchy or mesh for additional bandwidth savings. Squid consists of a main server program squid, a Domain Name System lookup program dnsserver, a program for retrieving FTP data ftpget, and some management and client tools. When squid starts up, it spawns a configurable number of dnsserver processes, each of which can perform a single, blocking Domain Name System (DNS) lookup. This reduces the amount of time the cache waits for DNS lookups. Squid is derived from the ARPA-funded Harvest project.

## sysklogd — (Version 1.3.31, 112K)

[B]

The sysklogd package contains two system utilities (syslogd and klogd) which provide support for system logging. Syslogd and klogd run as daemons (background processes) and log system messages to different places, like sendmail logs, security logs, error logs, etc.

## tcp_wrappers — (Version 7.6, 270K)

[W][S]

The tcp_wrappers package provides small daemon programs which can monitor and filter incoming requests for systat, finger, ftp, telnet, rlogin, rsh, exec, tftpd, talk and other network services. Install the tcp_wrappers program if you need a security tool for filtering incoming network services requests.

## tftp — (Version 0.10, 34K)

[W][S]

The Trivial File Transfer Protocol (TFTP) is normally used only for booting diskless workstations. The tftp package provides the user interface for TFTP, which allows users to transfer files to and from a remote machine. This program, and TFTP, provide very little security, and should not be enabled unless it is expressly needed. The TFTP server is run from /etc/inetd.conf, and is disabled by default on Red Hat Linux systems.

## timed — (Version 0.10, 74K)

[W][S]

The timed package contains the timed daemon and the timedc program for controlling the timed program. Timed synchronizes its host machine's time with the time on other local network machines. The timedc program is used to control and configure the operation of timed. Install the timed package if you need a system for keeping networked machines' times in synchronization.

## ucd-snmp — (Version 3.6.1, 1,504K)

[W][S]

SNMP (Simple Network Management Protocol) is a protocol used for network management (hence the name). The UCD-SNMP project includes various SNMP tools: an extensible agent, an SNMP library, tools for requesting or setting information from SNMP agents, tools for generating and handling SNMP traps, a version of the netstat command which uses SNMP, and a Tk/Perl mib browser. This package contains the snmpd and snmptrapd daemons, documentation, etc. Install the ucd-snmp package if you need network management tools. You will probably also want to install the ucd-snmp-utils package, which contains UCD-SNMP utilities.

## wu-ftpd — (Version 2.4.2b18, 398K)

[S]

The wu-ftpd package contains the wu-ftpd FTP (File Transfer Protocol) server daemon. The FTP protocol is a method of transferring files between machines on a network and/or over the Internet. Wu-ftpd's features include logging of transfers, logging of commands, on the fly compression and archiving, classification of users' type and location, per class limits, per directory upload permissions, restricted guest accounts, system wide and per directory messages, directory alias, cpath, filename filter and virtual host support. Install the wu-ftpd package if you need to provide FTP service to remote users.

## xntp3 — (Version 5.93, 968K)

The Network Time Protocol (NTP) is used to synchronize a computer's time with another reference time source. The xntp3 package contains utilities and daemons which will synchronize your computer's time to Coordinated Universal Time (UTC) via the NTP protocol and NTP servers. Xntp3 includes ntpdate (a program for retrieving the date and time from remote machines via a network) and ntpd (a daemon which continuously adjusts system time). Install the xntp3 package if you need tools for keeping your system's time synchronized via the NTP protocol.
