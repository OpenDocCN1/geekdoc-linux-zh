# v4.33
A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

With the file saved to /etc/rc.d/rc.firewall we start it by making the file
executable. The firewall script, if it exists and has executable permissions, will be called from /
etc/rc.d/rc.inet2. Check the permissions on the file, change them to executable (using
chmod) and check again. We can load the rules by simply calling the script explicitly:

```
root@forensic1:~# ls -l /etc/rc.d/rc.firewall
-rw-r--r-- 1 root 1195 Mar 12 2011 /etc/rc.d/rc.firewall
```

```
root@forensic1:~# chmod 755 /etc/rc.d/rc.firewall
```

```
root@forensic1:~# ls -l /etc/rc.d/rc.firewall
-rwxr-xr-x 1 root 1195 Mar 12 2011 /etc/rc.d/rc.firewall*
```

```
root@forensic1:~# sh /etc/rc.d/rc.firewall
```

With the last command in the session illustrated above, we have executed the firewall
script and now we look at our iptables configuration, we see the rules in place:

```
root@forensic1:~# iptables -S
-P INPUT DROP
-P FORWARD DROP
-P OUTPUT DROP
-A INPUT -i lo -j conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
-A INPUT -i eth0 -p tcp -m tcp --dport 22 --tcp-flags FIN,SYN,RST,ACK SYN -m
conntrack --ctstate NEW -j ACCEPT
-A OUTPUT -o lo -j ACCEPT
-A OUTPUT -o eth0 -j ACCEPT
```

Here we see the default policies (-P) are set to DROP and we have several rules in
chain. The lines starting with -A signify that we are applying a rule to our chain. Note
that our default policy is to drop all incoming traffic, and there is no explicit rule to allow
ing ICMP traffic, we can no longer ping our forensic workstation from an external host.
We can however, connect with SSH since we have a rule that accepts TCP traffic on
destination port 22 (assuming you un-commented the last line of the script and assuming the
SSH server is running on the default port)

```
bgrundy@hermes:~# ping 192.168.55.32
PING 192.168.55.32 (192.168.55.32) 56(84) bytes of data.
^C
--- 192.168.55.32 ping statistics ---
7 packets transmitted, 0 received, 100% packet loss, time 5999ms
```