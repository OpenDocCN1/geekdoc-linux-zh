is similar, but prints the name corresponding to *ipnumber*, which is the reverse of a normal lookup. (From now on, for brevity we'll use the term *hostaddr* to mean either a hostname or IP number.)

```
```
alice$ nslookup 198.186.203.20          (edited to save space)
Name:	klecker.debian.org
Address:	198.186.203.20
```
```

You can interrogate a DNS server other than the default using the command:

```
```
alice$ nslookup 198.186.203.20 res2.dns.uk.psi.net
Server:	res2.dns.uk.psi.net            use this DNS server to
Address:	154.32.107.18                resolve the IP address

Name:	klecker.debian.org
Address:	198.186.203.20
```
```

This is useful if you think there's a problem with your machine's configuration and you want to specify a server explicitly, or if you think your default server is misbehaving and you want to see how a different server handles the same query.

> > **Warning: if** `nslookup` **can't resolve the IP number of the server being used (specified in the resolver configuration, or explicitly as an IP number on the command line),** `nslookup` **fails completely. This is a big problem with** `nslookup`**.**

Irritatingly, `nslookup` has no "help" option that you can invoke from the command line. You have to go into interactive mode, and type `help` or `?`.

The `host` command is similar to `nslookup`. It doesn't have an interactive mode (but that doesn't matter) and is not available for Windows. We prefer it to `nslookup` because it's faster and its output is more informative, but its usage is very similar to `nslookup`'s.

```
```
host hostname                     what's the IP address for this name?

alice$ host www.debian.org
www.debian.org		A	198.186.203.20

host ipaddr                     what's the name for this IP address?

alice$ host 198.186.203.20
Name:	klecker.debian.org
Address:	198.186.203.20

host hostaddr serverhostaddr    use non-default DNS server

alice$ host 198.186.203.20 res3.dns.uk.psi.net
Name:	klecker.debian.org         use this DNS server
Address:	198.186.203.20
```
```

You can see that `host`'s output is less verbose, and because it doesn't print the address of the DNS server that's being used or try to resolve it, it's faster than `nslookup`.

So far we've covered the tip of the iceberg; what follows is the submerged mass. In the next two modules we examine in more detail the contents of DNS queries and replies, and how you can see them in more detail using `tcpdump`. Then in Modules 7.9 and 7.10 we see how advanced options in `nslookup` and `host` let you see this detail (without using `tcpdump`) and how exactly a name is being resolved.