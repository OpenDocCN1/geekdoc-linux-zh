After starting these services, use the **systemctl status** command to make sure the services are running. If you do not create the **iptables** file shown on the previous page, or if the service did not start for another reason, the output of this command will include the line **Active: inactive (dead)**.

With the **iptables** file shown above installed and the **iptables.service** unit started, the **iptables -L** option produces the following output:

```
```
# iptables -L
Chain INPUT (policy ACCEPT)
target     prot opt source               destination
ACCEPT     all  --  anywhere             anywhere             state RELATED,ESTABLISHED
ACCEPT     icmp --  anywhere             anywhere
ACCEPT     all  --  anywhere             anywhere
REJECT     all  --  anywhere             anywhere             reject-with icmp-host-prohibited

Chain FORWARD (policy ACCEPT)
target     prot opt source               destination
REJECT     all  --  anywhere             anywhere             reject-with icmp-host-prohibited

Chain OUTPUT (policy ACCEPT)
target     prot opt source               destination
```
```

You can use **systemctl** to turn off the **iptables** service:

```
```bash
# systemctl stop iptables.service
```
```

With the **iptables** service turned off, the **-L** option shows that no rules are in effect (and the system accepts all traffic):

```
```
# iptables -L
Chain INPUT (policy ACCEPT)
target     prot opt source               destination

Chain FORWARD (policy ACCEPT)
target     prot opt source               destination

Chain OUTPUT (policy ACCEPT)
target     prot opt source               destination
```
```

Give the command **service iptables save** to save the rules **iptables** is running. See the next section for more information.

**Emergency disconnect** An argument of **panic** severs all connections with the network. This command unloads all **iptables** modules from the kernel and sets a policy of DROP for all tables. It locks down the local system so no traffic can get in or out of it. Use this command if the system is under attack and you want to stop all network traffic in and out of the system immediately. Make sure you have backed up firewall rules you want to save before giving this command. See the caution tip on page 902.

```
```bash
# /usr/libexec/iptables/iptables.init panic
iptables: Flushing firewall rules:                      [ OK ]
iptables: Setting chains to policy DROP: filter          [ OK ]
```
```

# NOTES

**Startup** The **iptables** utility is a tool that manipulates rules in the kernel. It differs from daemons (servers) in its setup and use. Whereas Linux daemons such as Apache, vsftpd,