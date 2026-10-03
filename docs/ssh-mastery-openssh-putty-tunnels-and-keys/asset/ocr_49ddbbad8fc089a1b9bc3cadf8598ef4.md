convenient reference, that’s all.

To change the defaults, remove the pound sign and change the value.

# Multiple Values

Some environments need keywords set to multiple values. How you set those values depends on the keyword. Keywords like HostKey and Port can appear multiple times, each with a separate value.

```
Port 22
```

```
Port 2222
```

Keywords like Host accept multiple values, separated by a space.

```
Host envy.mwl1.io avarice.mwl1.io
```

Other keywords, such as Address, expect comma-separated values.

```
Address 192.0.2.0/25, 198.51.100.0/24
```

If ssh(1) or sshd(8) complains about a configuration, verify that you’re separating multiple entries correctly. This book contains many examples of assigning multiple values, but the OpenSSH manual is always the final word.

# Wildcards in OpenSSH Configuration Files

Configuration files for the OpenSSH server and client accept wildcards, called patterns. Rather than listing all possible values of a configuration setting, patterns let you say “anything that matches this expression.” Wildcards are most often used for Match rules, as discussed in “Conditional Configuration with Match” later this chapter. Patterns let you write configuration statements such as “all hosts in this domain” or “all IP addresses in this network.” The two wildcard characters are:

+   - ? matches exactly one character
- * matches zero or more characters

For example, I could use a pattern to set the value of the Host keyword to any host in mwl.io.

```
Host *.mwl1.io
```

If I used the question mark wildcard, this pattern would match any host with a one-character hostname. Very few environments segregate security domains by the length of the hostname, but if they did, you could use multiple question marks to identify them. This pattern matches sloth.mwl1.io and wrath.mwl1.io, but not gluttony.mwl1.io Or avarice.mwl1.io.

```
Host ????? .mwl1.io
```

Patterns are also useful for IP addresses. Here I match the hosts 203.0.113.10 through 203.0.113.19.

```
Address 203.0.113.?
```

If I use the asterisk wildcard, I can match any IP within a /24 network.

```
Address 203.0.113.*
```

You might use netmasks with IP address ranges, as discussed in Chapter 5. Negate patterns by putting an exclamation point in front. This pattern