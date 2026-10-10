# Chapter 22: Miscellaneous Servers



aspect of the servers’ behavior. In a more advanced configuration, you might integrate the DNS server with a DHCP server to dynamically update entries as IP addresses change, but such configurations are beyond the scope of this book.

> Tip
> 
> If you use a low-end broadband account for Internet access, outside services can link your dynamic IP address to a fixed hostname. Such dynamic DNS providers are common; check http://www.technopegan.org/dynamic/ or http://www.othnet.com/dynns.html for lists of such providers.

As a general rule, running your own DNS server for local use makes sense only when your network grows to over one or two dozen computers, assuming they need to address each other by name. If you’ve got just one or two servers and many clients, you might not need a DNS server; instead, you can configure the clients’ /etc/hosts files (or equivalents in other OSes, such as C:\WINNT\system32\drivers\etc\hosts in Windows 2000) to point to the servers.

> Note
> 
> Some protocols, such as the NetBIOS upon which Windows file sharing and Samba are built, use their own name resolution methods, so a DNS server may not be necessary if such tools are your primary reason for configuring a name server.

The most common DNS server in FreeBSD is the Berkeley Internet Name Domain (BIND). The server file’s name is named, and it’s installed as part of the base FreeBSD installation. If you prefer, you can run another server, such as djbdns or dns_balance (the former is available only as a port, but the latter is available as both a package and a port). Because BIND is the most popular DNS server for FreeBSD and because it’s installed by default, this chapter describes BIND configuration.

> Caution
> 
> This chapter emphasizes a basic BIND configuration, as might be suitable for a home or small business network. If your needs are more complex, you should consult a book on BIND, such as Albitz and Liu’s DNS and BIND, 4th Edition (O’Reilly, 2001). It’s easy to cause serious problems for your domain, and possibly for others, if BIND is misconfigured.

To actually run BIND, you should edit /etc/rc.conf so that it includes the following line:

```
named_enable="YES"
```

Adding this line makes BIND run when you next start the computer. You can type named as root to start it on a one-time basis after you create an initial configuration. If you make configuration changes, you have named reread its configuration files by typing killall -HUP named as root. Sometimes you may need to type killall named; named instead. This command shuts down BIND and restarts it, completely flushing its cache.