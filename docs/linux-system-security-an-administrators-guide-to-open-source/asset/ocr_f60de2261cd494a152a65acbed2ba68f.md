```
```bash
[root@topcat]# ipchains -A input -i eth1 -p tcp -s 10.0.0.0/8
1024:65535 -d 0/0 ftp-data -j ACCEPT
```
```

Once the packet passes this rule, it will go on to the forward chain. We already set up that rule in Masquerade Rule on page 476, so there is nothing further to do. The packet will pass through the forward chain, the source IP address being masqueraded, and then will go to the output chain. So we'll add that rule next.

# **FTP Rule 6.** This step is identical to **FTP Rule 2** except for the port. The rule is

```
```bash
[root@topcat]# ipchains -A output -i eth0 -p tcp -s topcat 1024:65535
-d 0/0 ftp-data -j ACCEPT
```
```

At this point the Internet ftp server can receive ftp-data requests from our internal client. Next we need to allow the server to respond to the request.

# **FTP Rule 7.** This step is identical to **FTP Rule 3** except that the port is ftp-data.

```
```bash
[root@topcat]# ipchains -A input -i eth0 -p tcp -s 0/0 21 -d topcat
1024:65535 -j ACCEPT ! -y
```
```

Once again, demasquerading occurs after this chain, the forward chain is skipped, and processing is passed to the output chain.

# **FTP Rule 8.** This rule is identical to **FTP Rule 4** except for the port.

```
```bash
[root@topcat]# ipchains -A output -i eth1 -p tcp -s 0/0 ftp-data -d
10.0.0.0/8 1024:65535 -j ACCEPT
```
```

We're done! Now users on the internal network can access the Internet via ftp (that was a lot of work—ask for a raise).

# **Allowing DNS, POP3, and Web Access** Conceptually, every rule required for these services is like that for ftp. The basic difference is that we won't have two distinct ports to deal with. DNS and POP3 do utilize both TCP and UDP, so we will need to deal with that. We'll cover each of the services in separate subsections.

# **DNS Rules.** We need to allow DNS queries from internal hosts and from topcat to reach the DNS servers in the Internet. The port number for DNS is 53 and its equivalent name from /etc/services is domain. Example 16-33 provides the necessary rules. Once again, we write the rules following the flow of events shown in Figure 16.4 on page 475. (The numbers to the left are for descriptive purposes.)

+   Rules 1 through 4 accept DNS queries from the internal network through eth1 in the input chain. Rules 5 through 8 allow those queries out to the Internet through eth0. Rules 9 through 11 allow the DNS responses to return through eth0. Note that once again we disallow TCP SYN packets. We