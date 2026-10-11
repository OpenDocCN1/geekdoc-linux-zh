```
```
  ipchains -P output REJET
  ipchains -P forward REJECT
```
```

The previous three commands set up a restrictive policy where you have to explicitly define the kinds of traffic that you want to allow through your firewall. Suppose that your security policy allows incoming mail, HTTP, and telnet connections from any public host. You enforce by adding the appropriate rule to the forward chain:

```
```
  ipchains -A forward -s 0.0.0.0/0 -d 38.110.200.0/24 -dport smtp -j$␷$
  ACCEPT
  ipchains -A forward -s 0.0.0.0/0 -d 38.110.200.0/24 -dport http -j$␷$
  ACCEPT
  ipchains -A forward -s 0.0.0.0/0 -d 38.110.200.0/24 -dport telnet -j$␷$
  ACCEPT

  ipchains -A forward -s 38.110.200.0/24 -d 0.0.0.0/0 -sport smtp -j$␷$
  ACCEPT
  ipchains -A forward -s 38.110.200.0/24 -d 0.0.0.0/0 -sport http -j$␷$
  ACCEPT
  ipchains -A forward -s 38.110.200.0/24 -d 0.0.0.0/0 -sport telnet -j$␷$
  ACCEPT
```
```

Note that the first three rules will match incoming connections, while the last three rules will match outgoing responses to those connections. Since you have only added rules to the forward chain, you're not yet allowing any connections to the Linux firewall itself. Perhaps you want to be able to telnet to the server for maintenance, but only from a known internal host of IP address 38.110.200.10 (ideally, the system administrator's workstation). The following two rules will allow this:

```
```
  ipchains -A input -s 38.110.200.10 -dport telnet -j ACCEPT
  ipchains -A output -d 38.110.200.10 -sport telnet -j ACCEPT
```
```

As with the previous example, you need to allow both incoming access for the telnet traffic, but also outgoing access for the responses.