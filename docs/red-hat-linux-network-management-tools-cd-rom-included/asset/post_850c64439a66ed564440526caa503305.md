
The **snmptrapd** command supports several command-line arguments: -P, -O, -d, and -q. The -P option will instruct **snmptrapd** to display any traps received on the standard output, and the -d option will display a dump of the trap packet. Thus, to show received traps and display the contents of trap packets, use the following command:

```
# snmptrapd -P -d
```

Executing this command, using the previous example on the host *rembrandt*, will display the following output:

```
1999-11-27 22:56:47 UCD-snmp version 4.0.1

received 69 bytes from 10.0.3.126:32566:
0000: 30 82 00 41 02 01 00 04 06 70 75 62 6C 69 63 43
00...public.
0016: 82 00 32 06 08 2B 06 01 04 01 03 01 01 40 04 0A
02...+......@
0032: 00 03 7E 02 01 02 02 01 00 43 03 24 5C 96 30 82
0..~..$..0
0048: 00 13 30 82 00 0F 06 0A 28 06 01 02 01 02 02 01
...0......
0064: 01 01 02 01 01
1999-11-27 22:56:51 monlet [10.0.3.126] enterprises.3.1.1:

Link Down Trap (O) Uptime: 6:37:09
interfaces.ifTable.ifEntry.ifIndex = 1
```

The first line shows the current version and when the **snmptrapd** process was run. Next, the output displays the number of bytes in the trap packet, the host the trap was sent from (*monlet*), and the UDP port (*32566*, in this case). The contents of the *trap* include both hexadecimal and ASCII characters. Finally, the trap information, including the variable-binding information, is shown.

The -d option will display additional debugging information that includes the parsing of MIB files. The -q option provides a more verbose output, but it doesn't seem to be implemented in this version of the command.

The **snmptrapd** command can be used as a focal point for reception of traps for a large number of devices. However, it must be running continuously in order to receive traps from the network. By default, this tool is not started by the system on startup. To enable this command on system startup, you should add it to the existing UCD agent startup script called *snmpd*. This shell script can be found in the
/etc/rc.d/init.d directory. Listing 8.2 shows the startup script with the snmptrapd command added on line number 21.

### Listing 8.2 UCD Startup Script with snmptrapd command

```
1  #!/bin/bash
2
3  # ucd-snmp init file for snmpd
4  #
5  chkconfig: - 50 50
6  # description: Simple Network Management Protocol (SNMP) Daemon
7  #
8  # processname: snmpd
9  # config: /etc/snmpd/snmpd.local.conf
10 # config: /etc/snmpd/snmpd.conf
11 # config: /usr/share/snmpd/snmpd.local.conf
12 # config: /usr/share/snmpd/snmpd.conf
13
14 # source function library
15 . /etc/rc.d/init.d/functions
16
17 case "$1" in
18     start)
19        echo -n "Starting snmpd: "
20        daemon /usr/sbin/snmpd -l /etc/snmpd/agent.log
21        daemon /usr/sbin/snmptrapd -s
22        touch /var/lock/subsys/snmpd
23        echo
24        ;;
25     stop)
26        echo -n "Shutting down snmpd: "
27        killproc snmpd
28        rm -f /var/lock/subsys/snmpd
29        echo
30        ;;
31     restart)
32        $0 stop
33        $0 start
34        ;;
35     status)
36        status snmpd
37        ;;
38     *)
39        echo "Usage: snmpd {start|stop|restart|status}"
40        exit 1
41 esac
42
43 exit 0
```

In this example, the script will be executed on system startup and the snmptrapd command will be invoked with the -s option (see line 21). This option enables the logging of messages to the syslog facility. Before messages can be received by syslog, however, the /etc/syslog.conf configuration file must be updated to
include an entry for trap processing. Listing 8.3 shows the standard Linux `syslog.conf` with the appropriate trap entry added (see line 25).

### Listing 8.3 Standard `syslog.conf` file with trap entry

```
1   # Log all kernel messages to the console.
2   # Logging much else clutters up the screen.
3   *kern.*
4       /dev/console
5
6   # Log anything (except mail) of level info or higher.
7   # Don't log private authentication messages!
8   *.info;mail.none;news.none;authpriv.none
9       /var/log/messages
10
11  # The authpriv file has restricted access.
12  authpriv.*
13      /var/log/secure
14
15  # Log all the mail messages in one place.
16  mail.*
17      /var/log/maillog
18
19  # Everybody gets emergency messages, plus log them on
20  # another machine.
21  *.emerg
22      /usr/bin/omail
23
24  # Save mail and news errors of level err or higher in a
25  # special file.
26  uucp,news.crit
27      /var/log/spooler
28
29  # Save boot messages also to boot.log
30  local7.*
31      /var/log/boot.log
32
33  local0.*
34      /var/log/trapd.log
35
36  #
37  # INN
38  #
39  news.crit
40      /var/log/news/news.crit
41  news.err
42      /var/log/news/news.err
43  news.notice
44      /var/log/news/news.notice
```

The new line defines the `syslog` entry that the **snmptrapd** uses when posting messages to the `syslogd` process. The entry indicates that all messages from the `local0` category will be collected. Note that all messages obtained will be saved to the `/var/log/trapd.log` file.

## Snmpwalk Tool

The **snmpwalk** command will *walk* an agent MIB tree using the SNMP getnext-request. Why use this command instead of the snmpget tool? Well, the snmpwalk command can discover the entire MIB tree contained within the agent automatically. With snmpget, you need to explicitly reference an object to obtain a value. With the snmpwalk command, you can start at a given point and move through the agent’s MIB to the end. An object variable may be given on the command line to specify with which portion of the MIB space the search will begin. Without an MIB object argument, snmpwalk searches and starts with the MIB-II object store. Thus, the command

```
# snmpwalk monet public
```

will walk the entire system agent on the device monet. Since MIB-II contains a large number of objects, the command will produce a rather long listing. Instead of listing every object supported by the agent, we can limit the search and display only a single group of objects. Thus, we can list all the objects found within the MIB-II system group using the following command:

```
# snmpwalk cisco-gw4 public system
```

Executing this command on the Cisco router generates the following sample output:

```
system .sysDescr.0 = Cisco Internetwork Operating System Software
IOS (tm) GS Software (RSP-JV-M), Version 11.1(13a)CA1, EARLY
DEPLOYMENT RELEASE SOFTWARE (fcl)
Synced to mainline version: 11.1(13a)
Copyright (c) 1986-1997 by cisco Systems, Inc.
Compiled Wed 13-Aug-97 04:12 by richardd
system .sysObjectID.0 = OID: enterprises .9 .1 .46
system.sysUpTime.0 = TimeTicks: (236153209) 27 days.
7:58:52.09
system .sysContact.0 = Susan Maxwell
system .sysName.0 = cisco-gw4
system.sysLocation.0 = Testing Lab
system .sysServices.0 = 78
```

To walk the entire MIB within a given agent and save the output to a file, use the following command:

```
# snmpwalk cisco-gw5 public .1 > walk.out
```

This command uses the .1 as the starting point to begin listing objects. Doing this will ensure that every object will be displayed because .1 is the root of the entire MIB tree and all objects are accessible from this point. Walking the entire MIB tree with an agent will help identify certain MIB objects or give you an idea of exactly how many objects a particular agent may support. To see the approximate number of objects the cisco-gw5 supports, count the number of lines in the file. Because the snmpwalk command displays each MIB object on its own line (unless the line is longer than the maximum number of characters for a line), we can then use the UNIX wc command to total the number of lines within the walk.out file. Thus, the command

```
# wc -l walk.out
```

produces the following output:

```
2242 walk.out
```

This command output shows that the agent contained within the cisco-gw5 device supports roughly 2242 MIB objects. When no object is specified with the snmpwalk command, it will search the MIB-II object tree by default. When the snmpwalk command reaches the end of the MIB within the agent, it will display the message End of MIB.

Note that the use of snmpwalk is a rather inefficient means to obtain a large number of MIB objects from an agent. This is because the command continuously queries a single MIB object to obtain an associated value. It is recommended that the snmpbulkwalk command be used whenever possible to reduce network traffic and load on the agent system. This command significantly reduces the work involved for a lower level to obtain a large amount of information from an agent. See the snmpbulkwalk section for additional information.

## Snmpbulkwalk Tool

The snmpbulkwalk tool communicates with a network entity using SNMPv2 bulk-request. Like the snmpwalk tool, snmpbulkwalk will
