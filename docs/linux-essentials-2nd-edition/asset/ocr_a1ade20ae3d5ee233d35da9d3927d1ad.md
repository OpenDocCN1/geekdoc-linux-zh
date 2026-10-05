# LISTING 11.3: Script demonstrating assignment and use of variables

```
#!/bin/bash
ip='route -n | grep UG | tr -s " " | cut -f 2 -d " "'
ping=/bin/ping"
echo "Checking to see if $ip is up..."
$ip -c 5 $ip
```

In practice, you use Listing 11.3 by typing the script's name. The result should
be the message Checking if see 192.168.1.1 is up (with 192.168.1.1
replaced by the computer's default gateway system) and the output from the
ping command, which should attempt to send five packets to the router. If the
router is configured to respond to pings, you will see five return packets
and summary information, similar to the following:

# $ routercheck

```
Checking to see if 192.168.1.1 is up...
PING 192.168.1.1 (192.168.1.1) icmp_seq=1 ttl=63 time=23.0 ms
64 bytes 192.168.1.1: icmp_seq=2 ttl=63 time=0.176 ms
64 bytes 192.168.1.1: icmp_seq=3 ttl=63 time=0.214 ms
64 bytes 192.168.1.1: icmp_seq=4 ttl=63 time=0.204 ms
64 bytes 192.168.1.1: icmp_seq=5 ttl=63 time=0.191 ms
```

```
-- 192.168.1.1 ping statistics----
5 packets transmitted, 0 received, 0% packet loss, time 4001ms
rtt min/avg/mdev = 0.176/0.758/23.005/9.123 ms
```

If the router is down, you'll see error messages to the effect that the host has
unreachable.
Listing 11.3 is of limited practical use and contains bugs. For instance, the
script identifies the computer's gateway by the presence of the string UG
in the router's output line from route. If a computer has two routers,
this won't work correctly, and the result is likely to be a script that misbehaves.
The purpose of Listing 11.3 is to illustrate how variables can be assigned and
not, to be a flawless working script.

Scripts like Listing 11.3, which obtain information from running or one
commands, are useful in configuring features that rely on system-specific infor-\mation or information that varies with time. You can use a similar approach to
obtain the current hostname (using the hostname command), the current time
(using date), the total time the computer's running (using uptime), free
disk space (using df), and so on. When combined with conditional expressions

> In addition to several
commands, the ip=
use back-ticks
(') to assign the
out of that-
chain to ip.
Chapter 8 describes this
technique.

![](bbox=[0.77, 0.135, 0.942, 0.175])