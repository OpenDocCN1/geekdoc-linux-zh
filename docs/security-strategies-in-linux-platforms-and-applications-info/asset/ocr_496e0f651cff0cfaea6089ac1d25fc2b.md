# PART 2 | Layered Security and Linux

Most kernel configurable files in the /proc/sys/ directory are boolean: in other words, they have a value of 0 or 1. If the file is active, its value is 1. So to activate IPv4 forwarding on a system, you would write the number 1 to the /proc/sys/net/ipv4/ip_forward file. One way to do this is with the following command:

```
# echo "1" > /proc/sys/net/ipv4/ip_forward
```

But the /proc/sys filesystem is dynamic. Changes to these files do not survive a reboot. To make changes permanent, you'll need to add appropriate options to the /etc/sysctl.conf file. The corresponding directive in that file is as follows:

```
net.ipv4.ip_forward = 1
```

You may note that there is no reference to proc or sys in that directive, as all kernel configuration options reside in the /proc/sys/ directory.
The following sections are based on a presentation by Steve Grubb of Red Hat at the 2008 Red Hat Summit. In that presentation, Grubb recommended kernel configuration changes in the areas described in these sections.
The focus of these sections is IPv4 networking. If you've also enabled Internet Protocol version 6 (IPv6) networking, don't forget to make parallel changes to matching directories in the /proc/ filesystem and matching directives in the /etc/sysctl.conf file.

# Don't Reply to Broadcasts

Normally, a system will respond to a ping command addressed to the broadcast address of a network. For example, the following command should receive responses from all systems with IP addresses on the 192.168.0.0/24 network:

```
$ ping -b 192.168.0.0.255
```

A black-hat hacker who can identify the IP address of a system can start attacking that system. A black-hat hacker who can identify the IP addresses of all systems on a network can attack those systems simultaneously. To prevent that, you'd activate the following option:

```
/proc/sys/net/ipv4/icmp_echo_ignore_broadcasts
```

As suggested by the name, the option ignores broadcast messages using Internet Control Protocol (ICMP). It works because the ping command uses ICMP. The corresponding option in /etc/sysctl.conf is as follows:

```
net.ipv4.icmp_echo_ignore_broadcasts = 1
```

This option does not prevent responses to targeted ping commands, but broadcasts. One advantage is that it also prevents what is known as a smurf attack, where a broadcast is sent using a spoofed or faked source address of the intended target computer.