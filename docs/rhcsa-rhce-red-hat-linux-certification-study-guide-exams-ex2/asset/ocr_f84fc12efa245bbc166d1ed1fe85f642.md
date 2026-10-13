# FIGURE 2-18 [root@server1 ~]# nmap localhost

Apply a port scanner locally

```
Starting Nmap 5.21 ( http://nmap.org ) at 2010-11-29 09:47 PST
mass_dns: warning: Unable to determine any DNS servers. Reverse DNS is disabled.
Try using --system-dns or specify valid servers with --dns-servers
Nmap scan report for localhost (127.0.0.1)
Host is up (0.000070s latency).
Hostname localhost resolves to 2 IPs. Only scanned 127.0.0.1
Not shown: 997 closed ports
PORT     STATE SERVICE
22/tcp   open  ssh
25/tcp   open  smtp
111/tcp  open  rpcbind

Nmap done: 1 IP address (1 host up) scanned in 0.07 seconds
[root@server1 ~]#
```

# Configure an E-Mail Client

The configuration process for a GUI e-mail client should be trivial for any candidate for Red Hat certification. However, the same may not necessarily be true for command line clients, and they're useful for testing the functionality standard e-mail server services such as Postfix and sendmail. For example, once a server is configured for Post Office Protocol (POP) e-mail, even e-mail that is delivered using the near ubiquitous version 3 (POP3), it can be checked with the following command:

```
# mutt -f pop://username@host
```

Since GUI e-mail clients should be trivial for readers, the remainder of this section is focused on the use of command line e-mail clients.

# Command Line Mail

One way to test a local mail system is with the built-in command line mail utility. It provides a simple text-based interface. The system keeps each user's mail in /var/mail directory associated with each username. Users who read messages with the mail utility can also reply, forward, or delete associated messages.

You can certainly use any of the other mail readers, such as mutt, or the e-mail managers associated with different GUI web browsers to test your system. Other mail readers store messages in different directories. For example, the pine utility would