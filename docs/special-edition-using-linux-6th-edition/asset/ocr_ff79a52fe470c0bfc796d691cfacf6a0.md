```
WARNING: Unauthorized entry into this system for any reason is
a criminal act and will be prosecuted to the fullest extent of the law.

option:  ALLOW
access:  granted
```

Testing a non-local client for telnet access, you receive the following:

```
client:   hostname locus2.caldersystems.com
client:   address   207.179.18.140
server:   process in.telnetd
matched:  hosts.allow line 7
option:   DENY
access:   denied
```

Creating a few more hypothetical matches shows that the rules you’ve created do what you want. Just remember that only those TCP services administered by inetd are protected in this way. Other services that do not run out of inetd or UDP services must be protected by other means, such as netfilter.