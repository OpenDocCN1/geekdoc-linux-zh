# ps: monitor processes

Implementations of ps have become hopelessly complex over the last decade. Vendors have abandoned the attempt to define meaningful displays and make their pses completely configurable. With a little customization, almost any desired output can be produced. As a case in point, the ps used by Linux is a triaxial and hermaphroditic version that understands multiple option sets and uses an environment variable to tell it what universe it's living in.

Do not be alarmed by all this complexity; it's mainly for developers, not for system administrators. Although you use ps frequently, you only need to know a few specific inc.

On Linux and AIX, you can obtain a useful overview of all the processes running on the system with ps aux. The option means to show all processes, x means to show even processes that don't have a control terminal, and u selects the "oriented" format. Here's an example of ps aux output on a machine-running Red Hat (AIX output for the same command differs slightly):

# redhat ps aux

| USER PID %CPU%MEM VZ RSS TTY TIME COMMAND |
|---|---|---|---|---|---|---|---||
| root | 1 | 0.1 0.2 3356 560 | ? | S | 0:00 | init [5] |
| root | 2 | 0 0 | ? | SN | 0:00 | [kthread/0] |
| root | 3 | 0 0 | ? | Sc | 0:00 | [events/0] |
| root | 4 | 0 0 | ? | Sc | 0:00 | [khelper] |
| root | 5 | 0 0 | ? | Sc | 0:00 | [kacpid] |
| root | 18 | 0 0 | ? | Sc | 0:00 | [blockd/0] |
| root | 28 | 0 0 | ? | S | 0:00 | [pdflush] |
| root | 196 | 0 0 | ? | S | 0:00 | [journald] |
| root | 1050 | 0 0.1 2652 448 | Scs | 0:00 | udevd |
| root | 1472 | 0 0.3 3048 1008 | Scs | 0:00 | /sbin/dhclient -1 |
| root | 1646 | 0 0.3 3012 1012 | Scs | 0:00 | /sbin/dhclient -1 |
| root | 1733 | 0 0 | ? | S | 0:00 | [journald] |
| root | 2124 | 0 0.3 3004 1008 | Ss | 0:00 | /sbin/dhclient -1 |
| root | 2182 | 0 0.2 2294 596 | Ss | 0:00 | syslogd -m |
| root | 2186 | 0 0.1 2952 484 | Ss | 0:00 | klod -x |
| rpc | 2207 | 0 0.2 2824 580 | Ss | 0:00 | portmap |
| rpcuser | 2227 | 0 0 2100 760 | Ss | 0:00 | rpc.statd |
| root | 2260 | 0 0.4 5668 1084 | Ss | 0:00 | rpc.idmapd |
| root | 2336 | 0 0.2 3268 555 | Ss | 0:00 | /usr/sbin/acpid |
| root | 2348 | 0 0.8 9100 1660 | Ss | 0:00 | cupsd |
| root | 2384 | 0 0.6 4080 1660 | Ss | 0:00 | /usr/sbin/sshd |
| root | 2399 | 0 0.3 2780 828 | Ss | 0:00 | xineted-staylive |
| root | 2419 | 0 1.1 7776 3004 | Ss | 0:00 | sendmail: accept |

![](bbox=[0.235, 0.285, 0.275, 0.33])

Command names in brackets are not really commands but rather kernel threads scheduled as processes. The meaning of each field is shown in Table 5.4 on the next page.

Another useful set of arguments for Linux and AIX is lax, which provides more technical information. The a and x options are above (every process),