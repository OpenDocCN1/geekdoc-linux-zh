A good example of why you might want to limit based on IP address is an intranet site, like an internal wiki. If you use a wiki for your internal documentation, you probably don’t want the entire world to read it. You might even host a wiki just for a particular group of users and want to restrict access so that only their network can see it. When you define more advanced ufw rules, you must use the extended ufw syntax. This syntax requires you to specify the protocol and port number explicitly, so you can’t use the same shortcuts as in the simpler commands. Here’s an example command to limit Web access (port 80) to just the 10.1.1.0 network:

```
$ sudo ufw allow proto tcp from 10.1.1.0/24 to any port 80
```

Let’s break this command down. The proto tcp section defines whether this rule applies to TCP or UDP. I limit what networks this rule applies to with from 10.1.1.0/24. The to any port 80 section of the command says that this rule applies to port 80 on any destination address on the machine.

Even if you deny by default, there might be circumstances when you also add a deny rule. For instance, let’s say that you are running an external SMTP (mail) server and you notice that a host inside your network at 10.1.1.75 appears to be infected with a virus and is flooding your mail server with invalid messages. To block just that IP address, you would type

```
$ sudo ufw deny proto tcp from 10.1.1.75 to any port 25
```

If you wanted to block all packets from that host, not just SMTP, you wouldn’t need to define the proto or to arguments:

```
$ sudo ufw deny from 10.1.1.75
```

Later on, once the virus has been removed and the host is back to normal, you can remove the rule with

```
$ sudo ufw delete deny proto tcp from 10.1.1.75 to any port 25
```

or, if you dropped all packets from the host, this command would remove it:

```
$ sudo ufw delete deny from 10.1.1.75
```