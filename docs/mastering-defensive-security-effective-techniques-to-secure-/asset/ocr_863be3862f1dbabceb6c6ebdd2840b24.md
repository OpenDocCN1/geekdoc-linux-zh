# SSH brute-force protection with iptables

You can use the following iptables rules to block IP addresses that attempt more than a given number of SSH connections in X seconds. Here is an example to block an IP address if there are more than eight SSH connections in 45 seconds:

```
iptables -A INPUT -p tcp --dport ssh -m conntrack --ctstate NEW
-m recent --set
iptables -A INPUT -p tcp --dport ssh -m conntrack --ctstate NEW
-m recent --update --seconds 45 --hitcount 8 -j DROP
```

Notice the first command is used to track new connections coming in on port 22 (SSH), while the second command tells iptables to drop packets from a given IP address that has sent eight or more requests in 45 seconds.

> Note
If you want to insert these two rules at the top of your INPUT chain (to trigger them before the rest of yours), use -I instead of -A as the first parameter.

Another good option is to whitelisting as this enables you to allow one or more IPs to access your server while dropping everything else.

Here is the command to use this technique:

```
iptables -I INPUT -p tcp -s 10.10.10.10,192.168.1.14 --dport ssh
ssh -j ACCEPT
iptables -I INPUT -p tcp --dport ssh -j DROP
```

The preceding example will allow SSH connections ONLY from those two IP addresses while blocking any access from any other IP address.

# Protecting from port scanning with iptables

There are several ways to protect from port scanning with iptables, however, this is my favorite:

```
iptables -N PORT-PROTECT
iptables -A PORT-PROTECT -p tcp --syn -m limit --limit 2000/
hour -j RETURN
iptables -A PORT-PROTECT -m limit --limit 200/hour -j LOG
--log-prefix "DROPPED Port scan: "
```