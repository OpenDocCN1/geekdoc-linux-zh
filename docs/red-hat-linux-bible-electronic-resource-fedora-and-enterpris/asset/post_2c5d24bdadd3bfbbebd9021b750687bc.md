
Unless you are a TCP/IP expert, you're probably wondering what services these ports represent. The Internet Assigned Numbers Authority (IANA) assigns services to UDP and TCP ports. You can see these assignments at the following Web address:

```
www.iana.org/assignments/port-numbers
```

Network services in Red Hat Linux (as well as other Linux/UNIX systems) obtain port number assignments from the /etc/services file. So, in general, you can simply check the /etc/services file to find out most of the services that are assigned to ports being scanned.

Ports assigned for monitoring are chosen based on a couple of different criteria. Lower port numbers (1, 11, 15, etc.) are chosen to catch port scanners that begin at port 1 and scan through a few hundred ports. If the scanner is blocked after accessing port 1, it won't be able to get information about any other ports that may be open on your computer. Another criterion is to include ports that are checked specifically by intruders because those services may be vulnerable to attack. They include the systat (port 11) and netstat (port 15) services.

You will want to remove ports from the list in the portsentry.conf file if you are actually running the service assigned to that port. On the other hand, you may want to add ports to the list if you are paranoid about attacks and you want a bit more coverage. The portsentry.conf file contains some examples that you can uncomment (remove the # sign) so that more ports are monitored.

If you change from basic to stealth scans (as described in the "Changing the portsentry modes file" section, later in this chapter), the ports that are monitored are those defined by the ADVANCED_PORTS_TCP and ADVANCED_PORTS_UDP options. Here is how those two options are set by default:

```
ADVANCED_PORTS_TCP="1023"
ADVANCED_PORTS_UDP="1023"
```

The two preceding entries indicate that all ports from 1 to 1023 are monitored. Monitoring higher port numbers can result in many more false alarms, so this practice is not recommended. If you find that PortSentry is being tripped accidentally, you may want to exclude the ports being tripped by using the ADVANCED_EXCLUDE_TCP and ADVANCED_EXCLUDE_UDP options. The following example shows how these two values are set by default:

```
ADVANCED_EXCLUDE_TCP="111,113,139"
ADVANCED_EXCLUDE_UDP="520,138,137,67"
```

By default, ident and NetBIOS services for TCP (ports 111, 113, and 139) and route, NetBIOS, and Bootp broadcasts for UDP (ports 520, 138, 137, and 67) are excluded from the advanced scan. (The exclusion is because a remote computer may hit these ports without representing any misuse.) If you are running in stealth mode, you should likewise exclude any services that you are running on your system by adding their port numbers to this list.

## Identifying configuration files

Besides the `portsentry.conf` file, there are several other configuration files used by PortSentry. You can identify the locations of these other files within the `portsentry.conf` file. Here are how those files are defined:

```
# Hosts to ignore
IGNORE_FILE="/etc/portsentry/portsentry.ignore"
# Hosts that have been denied (running history)
HISTORY_FILE="/var/portsentry/portsentry.history"
# Hosts denied this session only (temporary until next restart)
BLOCKED_FILE="/var/portsentry/portsentry.blocked"
```

Chances are that you will not want to move the location of these configuration files. Here are some descriptions of what these files are used for:

- The `portsentry.ignore` file contains a list of all IP addresses that you do not want blocked (even if they improperly try to access ports on your computer). By default, all IP addresses assigned to the local computer are added to this file. You can add IP addresses of trusted computers, if you like.
- The `portsentry.history` file contains a list of IP addresses for computers that have been blocked from accessing your computer.
- The `portsentry.blocked.*` files contain a list of computers that have been blocked from accessing your computer during the current session. The `portsentry.blocked.tcp` file contains IP addresses of computers that have improperly scanned TCP ports on your computer. Addresses of computers that have been blocked after scanning UDP ports are contained in the `portsentry.blocked.udp` file.

Access to ports on your computer is only blocked during the current session (that is, until the next reboot or restart of PortSentry). So, to more permanently exclude remote computers, you should impose other restrictions (such as by using the `/etc/hosts.deny` file, a firewall command, or a route to a dead host). These methods are described later in this chapter.

## Choosing responses

Someone scanning a port is like them checking a door in your house to see if it is locked. In most cases, it indicates that someone is checking your system for weaknesses. That is why, when another computer scans your ports, the default response from PortSentry is to block further access from the other computer to your computer for the duration of the current session. No action is taken to permanently block access from that computer. The `BLOCK_UDP` and `BLOCK_TCP` options in the `portsentry.conf` file set which type of automatic response is taken when ports are scanned. Here is how these options are set by default:

```
BLOCK_UDP="2"
BLOCK_TCP="2"
```

The value in quotation marks determines how PortSentry reacts to a scan of your ports by another computer. The following list describes each of these values.

- A value of "2" (the default value) causes access to be temporarily blocked to services for the scanned protocol (TCP or UDP) and for the action to be logged. Also, if any commands were defined to be run by a `KILL_RUN_CMD` option, that command is then run. (This option is not configured by default.)
- A value of "0" causes port scans to be logged, but not blocked.
- A value of "1" causes the `KILL_ROUTE` and `KILL_HOSTS_DENY` options to be run. (See the following list for descriptions of these options.) By default, further requests from the remote computer will be rerouted to a dead host, and the remote host's IP address will be added to the `/etc/hosts.deny` file, thereby denying access to network services.

Following are some suggestions on options you can use to change the responses to your ports being scanned:

- `KILL_ROUTE`: This option runs the `/sbin/route` command to reroute requests from the remote computer to a dead host. By default, this option is set to the following value, which effectively drops the request from the remote computer:
  `KILL_ROUTE="/sbin/route add -host $TARGETS gw 127.0.0.1"`

> **NOTE:** Instead of rerouting IP packets from the remote host, you can use firewall rules to deny access. If you use `ipchains` firewalls, uncomment the following line to deny access from the remote host. If you are using `iptables`, change `ipchains` to `iptables` and create an appropriate `iptables` response.

```
KILL_ROUTE="/sbin/ipchains -I input -s $TARGETS -j DENY -l"
```

This `ipchains` rule would deny (in other words, drop) all packets from the remote computer. To make this action permanent, you could add the `ipchains` options (from the -I to the end of the line) to the `/etc/sysconfig/ipchains` file, replacing the `$TARGETS` with the actual IP address of the computer you want to deny access to.

- `KILL_HOSTS_DENY`: This option is used to deny requests for any network services that are protected by TCP wrappers. This option is set by default as follows:
  `KILL_HOSTS_DENY="ALL: $TARGETS"`

With the preceding option set, `$TARGETS` is replaced by the IP address of the intruding remote computer and the line in quotes is added to the `/etc/hosts.deny` file. For example, if the remote computer's IP address were 10.0.0.59, the line that appears in `/etc/hosts.deny` would be:

```
ALL: 10.0.0.59
```

- `KILL_RUN_CMD`: Instead of using firewalls, rerouting, or TCP wrappers to deny an intruding computer from accessing your computer, you can choose any command you like in response. With the BLOCK_TCP and BLOCK_UDP options set to “2”, the value of KILL_RUN_CMD is run in response to a scan of your monitored ports.

The value of KILL_RUN_CMD should be the full path to the script you want to run, plus any options. To include the IP address of the remote computer or the port number that was scanned, you could include the $TARGET$ or $PORT$ variables, respectively. Here is how the example appears that you would want to modify:

`KILL_RUN_CMD="/some/path/here/script $TARGET$ $PORT$"`

> **CAUTION**: Do not use any KILL_RUN_CMD to retaliate against the intruding remote host. Firstly, it is quite possible that the computer that is scanning your ports has itself been cracked and is thus not a valid target for retaliations, and secondly, retaliation may simply incite the cracker into further attacks on you.

- `PORT_BANNER`: You can send a message to the person who sets off the PortSentry monitor by setting the PORT_BANNER option. By default, no message is defined. However, you can uncomment the following line to use that message. (An abusive message is not recommended.)

`PORT_BANNER="** UNAUTHORIZED ACCESS PROHIBITED *** YOUR CONNECTION ATTEMPT HAS BEEN LOGGED. GO AWAY."`

The number of scans from an intruding computer that PortSentry will accept before setting off the responses described above can be set by using the SCAN_TRIGGER option. By default, that option is set as follows:

`SCAN_TRIGGER="0"`

The “0” value means that you won’t accept any scans from an intruding system. In other words, the first scan will trip the PortSentry monitor. You can increase this value to be tolerant of one or more errant scans (though you probably won’t want to).

## Changing the portsentry.modes file

The /etc/portsentry/portsentry.modes file defines the modes in which the PortSentry command is run at boot time. Here is how that file appears by default:

```
tcp
udp
#stcp
#sudp
#atcp
#audp
```

The tcp and udp options are the basic PortSentry modes for the TCP and UDP services, respectively. Your other choices of options include stealth TCP (stcp) and advanced stealth
