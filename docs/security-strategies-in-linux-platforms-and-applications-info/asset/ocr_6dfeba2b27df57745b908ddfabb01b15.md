# 186 PART 2 | Layered Security

+   - - j LOG—The packet is logged: other - j switches may specify actions that may follow.
- - j ACCEPT—The packet is accepted, and is sent to the destination specified in the header of the packet.

Sample iptables Commands
With the iptables options shown, you should be able to understand several different kinds of commands. As an example, Figure 7-1 shows an excerpt of the Red Hat /etc/sysconfig/iptables configuration file. These options are added to the iptables command during the boot process. If you are administering Red Hat systems, pay careful attention. Some of these rules may not be necessary for your configuration. In fact, many firewalls include hundreds of iptables commands. Such complexity can lead to errors. In many cases, fewer iptables rules lead to a more secure system.

> FYI

While this discussion is based on a Red Hat iptables configuration file, similar guidelines apply to Ubuntu-based configuration files. One example, based on Ubuntu’s uncomplicated (ufw) package, stores comparable configuration files in the /etc/ufw/ directory.
While the iptables chain used for Red Hat systems is normally named RH-Firewall-1-INPUT, that’s just a label. If you use the ufw package, you will end up with several different chains. For that reason, this section is focused on the Red Hat based firewalls.

```
:RH-Firewall-1-INPUT [0:]
-A INPUT -j RH-Firewall-1-INPUT
-A FORWARD -j RH-Firewall-1-INPUT
-A RH-Firewall-1-INPUT -p icmp --icmp-type any -j ACCEPT
-A RH-Firewall-1-INPUT -p 50 --dport 139 -j ACCEPT
-A RH-Firewall-1-INPUT -p tcp --dport 22 -j ACCEPT
-A RH-Firewall-1-INPUT -p udp --dport 5353 --dport 424:0:251 -j ACCEPT
-A RH-Firewall-1-INPUT -p tcp --dport 6343 -j ACCEPT
-A RH-Firewall-1-INPUT -m state ESTABLISHED,RELATED -j ACCEPT
-A RH-Firewall-1-INPUT -m state NEW -m tcp -p tcp --dport 2049 -j ACCEPT
-A RH-Firewall-1-INPUT -m state NEW -m tcp -p tcp --dport 443 -j ACCEPT
-A RH-Firewall-1-INPUT -m state NEW -m tcp -p tcp --dport 22 -j ACCEPT
-A RH-Firewall-1-INPUT -m state NEW -m udp -p udp --dport 137 -j ACCEPT
-A RH-Firewall-1-INPUT -m state NEW -m udp -p udp --dport 138 -j ACCEPT
-A RH-Firewall-1-INPUT -m state NEW -m udp -p udp --dport 137 -j ACCEPT
-A RH-Firewall-1-INPUT -m state NEW -m tcp -p tcp --dport 445 -j ACCEPT
-A RH-Firewall-1-INPUT -m state NEW -m tcp -p tcp --dport 80 -j ACCEPT
-A RH-Firewall-1-INPUT -m state NEW -m udp -p udp --dport 161 -j ACCEPT
-A RH-Firewall-1-INPUT -m state NEW -m udp -p udp --dport 902 -j ACCEPT
COMMIT
-A RH-Firewall-1-INPUT -j REJECT reject-with icmp-prohibited
```

FIGURE 7-1

 Firewall rules from
/etc/sysconfig/iptables.*