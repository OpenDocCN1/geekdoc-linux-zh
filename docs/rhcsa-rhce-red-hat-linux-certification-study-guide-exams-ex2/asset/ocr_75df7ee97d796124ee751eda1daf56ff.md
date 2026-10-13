# FIGURE 4-4

Default RHEL 6 firewall rules

```
[root@server1 ~]# iptables -L
Chain INPUT (policy ACCEPT)
target     prot opt source               destination
ACCEPT     all  --  anywhere             anywhere             state RELATED,ESTABLISHED
ACCEPT     icmp --  anywhere             anywhere
ACCEPT     all  --  anywhere             anywhere
ACCEPT     tcp  --  anywhere             anywhere             state NEW tcp dpt:ssh
REJECT     all  --  anywhere             anywhere             reject-with icmp-host-prohibited

Chain FORWARD (policy ACCEPT)
target     prot opt source               destination
REJECT     all  --  anywhere             anywhere             reject-with icmp-host-prohibited

Chain OUTPUT (policy ACCEPT)
target     prot opt source               destination
[root@server1 ~]#
```

Six columns of information are shown in Figure 4-4, which correspond to various iptables command options. The firewall shown is based on the following rules listed in the /etc/sysconfig/iptables file. The first line specifies that the rules to follow are filtering rules. Alternative rules support Network Address Translation (NAT) or mangling; NAT is discussed in Chapter 10.

```
*filter
```

Next, network traffic that is directed to the local system, intended to be forwarded, and are sent out, are normally accepted by default with the ACCEPT option.

```
:INPUT ACCEPT [0:0]
:FORWARD ACCEPT [0:0]
:OUTPUT ACCEPT [0:0]
```

Some security professionals, including the U.S. National Security Agency, suggest that the ACCEPT should be changed to DROP for at least the INPUT and FORWARD lines. If you accept this recommendation, packets that aren't explicitly accepted by other rules are automatically dropped. However, that level of security may be covered in Red Hat's Enterprise Security Network Services course (RHS333), which is open to those who have already passed the RHCE exam. The [0:0] are byte and packet counts, which each start at 0.

The lines that follow are all applied to the iptables command. Every switch and option listed in this file should be available on the associated man page.

The next line keeps current network communications going. The ESTABLISHED option continues to accept packets on current network connections. The RELATED