Based on the conditions given, you'd change that directive to

```
define(`SMART_HOST', `maui.example.com')dnl
```

# Lab 7

This lab is quite similar to Lab 2. While there are options in the sendmail configuration files, the most efficient way to limit access to a specific network is still with an appropriate iptables-based firewall rule. The rule discussed in the answer to Lab 2 would also work in this case. Alternatively, you can configure access limits in the /etc/mail/access file, such as

```
Connect: 192.168.122 OK
Connect: 192.168.100 REJECT
```