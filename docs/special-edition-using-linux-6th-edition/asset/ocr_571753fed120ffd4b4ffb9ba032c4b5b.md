# IMPLEMENTING THE POLICIES

Now all that’s left is to implement the policies. Declare a few variables because this reduces errors. Follow these steps:

Use the following names, which are similar to the ones in the previous summary:

```
fooint=209.191.169.1/25        # this is eth0
fooext=209.191.169.129/25      # this is eth1
```

+   1. Start with a clean slate:
+   
+   ```bash
+   iptables -F
+   iptables -t mangle -F
+   iptables -t nat -F
+   iptables -X
+   iptables -t mangle -X
+   iptables -t nat -X
+   ```

+   2. Stop pings and scans that come from outside:
+   
+   ```bash
+   iptables -N scans
+   iptables -A scans -m state --state INVALID -j DROP
+   iptables -A scans -m unclean -j DROP
+   iptables -A scans -p icmp --icmp-type echo-request -i eth1 -j DROP
+   iptables -A INPUT -j scans
+   iptables -A FORWARD -j scans
+   ```

+   3. Now pass all traffic from inside out (except nntp):
+   
+   ```bash
+   iptables -N passthis
+   iptables -N blockthis
+   iptables -A passthis -s fooint -p icmp -i eth0 -j ACCEPT
+   iptables -A passthis -s fooint -p tcp --sport 119 -d 0/0 -i eth0 -j ACCEPT
+   iptables -A blockthis -s fooint -p tcp --sport 119 -j REJECT --reject-with icmp-port-unreachable
+   iptables -A FORWARD -j passthis
+   iptables -A OUTPUT -j passthis
+   ```

+   4. Block those pesky services that are a common security problem or that you just don’t want, such as telnet and imap:
+   
+   ```bash
+   iptables -A blockthis -i eth1 -s 0/0 -d fooint -p tcp --sport 23 -j DROP
+   iptables -A blockthis -i eth1 -s 0/0 -d fooint -p tcp --sport imap -j DROP
+   iptables -A FORWARD -j blockthis
+   ```

You really don’t need to specify eth1 because if it came from eth0, you’ve already accepted it previously and, therefore, you won’t get the chance to drop it. In fact, a number of the rules here have some information duplicated, but this project is intended to show examples of rules and how to put them together.

+   5. Be sure to accept DNS (on fooint only), ssh, and returns on most upper ports (and on both networks), but drop any requests from outside for XDM or X access:
+   
+   ```bash
+   iptables -I passthis 1 -m state --state ESTABLISHED,RELATED -j ACCEPT
+   iptables -A passthis -i eth0 -p tcp -s fooint -d 0/0 --dport domain -j ACCEPT
+   iptables -A passthis -i eth0 -p udp -s fooint -d 0/0 --dport domain -j ACCEPT
+   iptables -N passthisin
+   iptables -A passthisin blockthis
+   iptables -A passthisin -p tcp --dport 22 -j ACCEPT
+   ```