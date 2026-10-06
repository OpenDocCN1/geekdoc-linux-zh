# 462 Part III ♦ Choosing and Installing a Linux Distribution

The Fedora Core and RHEL Firewall Configuration screen handles almost everything
t average desktop user needs in a firewall. Here is what you can do with the set-
t on that page:

+   **No firewall** — Although this option is not generally recommended, some people-choose No firewall if they are directly connected to a router firewall or feel
no threat from their network connection. This allows connection requests
to all ports. Requests to configured services are allowed, while
requests for other services are ignored. The firewall just passes these
requests without question.

+   **Enable firewall** — Select this option to set up a basic set of iptables
rules for you, without having to figure out how iptables works. If you are
offering services to share web pages (WWW/HTTP), FTP server (FTP), remote
copy login services (SSH), or a mail server (SMTP), you can simply click
boxes to begin those services.

+   **Other ports** — Although not in Fedora Core 3, earlier versions of Red Hat
Linux allows you to add the port numbers associated with other
ervices in an "other ports" field. If the Red Hat distribution you are installing
as that field available, you can simply add a port number or associate a par-
ticular port with a protocol, using the port name or followed by a
colon and the protocol name. Here's the Red Hat gives:

```
imap:tcp
```

This enables requests from your network for IMAP services (port 143) from
TCP protocols. You can also add multiple ports by separating them by com-mas. For example, the following entry enables the computer to be a domain
name server or to serve up mailboxes without opening ports.

```
53, 110
```

Open your IMAP and POP3 ports only if your computer is a mail server. If you're
just downloading and reading mail from your computer, you can get just mail
fine from an IMAP or POP3 without opening ports.

+   **Select network devices** — Another feature in Red Hat Linux, before Fedora
Core 3, is a select network devices box that displayed interfaces associated
network cards on your computer. For Ethernet devices, you can use eth0, eth1,
and so on (for each card found). If you want to accept all requests made
of one from those interfaces, select the check box next to it. For example, if
you plan to deal out (pppp0) to get the Internet but have a connection
to your LAN (eth0) that you plan to share your Internet connect-ion, with select eth0.

Once Fedora or RHEL is installed, run the system-config-securitylevel
command to open the Security Level Configuration window. That window pro-\vidas a to select trusted network devices and add accessible ports (by name
number) to your iptables firewall.