
**Exercise 2:** change your DNS configuration so that the first DNS server in the list doesn't exist. (Use something like 10.10.10.123 or some other number from a private address set that you know isn't in use on your network. Make sure it is not an address in your local segment's range or you will see only failing ARPs.) Now try the **ping** again. Do you see any pattern in the intervals between successive DNS attempts? Now try two non-existent servers, and then all non-existent servers.

## 7.5 Lab – configuring your Windows PC to use DNS

Now we’ll do the basic DNS configuration for a PC on a typical small site connected to the Internet that relies on the DNS servers operated by the site’s ISP and has no internal DNS servers.
The only settings you *must* enter are one DNS server address and the hostname; if you don’t enter at least one server address your PC won’t use DNS. (Windows automatically fills in the hostname. See Module 8.14 for more detail. It is Windows that insists you enter a name here; DNS doesn’t care.)

Enter the IP number of the DNS server(s): Control Panel > Network > Protocols > TCP/IP > DNS > DNS Service Search Order > Add ... (Figure 7.5).

![](img/a2132b646d336d5f9a21102d6320e537_219_0.png)

You can enter up to three servers. As with Linux, servers closer to the top of the list are used first; the **Up** and **Down** buttons let you change the order of the servers, so you can set your own preference for the order in which the servers are used. Modified settings take effect as soon as you press **OK** or **Apply**; you don’t have to reboot. (**Apply** is the same as **OK** but it doesn’t close the window. **Apply** is useful when you are experimenting with the settings: if you leave the Network window and come back to it, it will be open at the appropriate place.)
As usual you can verify the changes using *ipconfig/all* (Figure 7.6) or *winipcfg* (Figure 7.7).

![](img/a2132b646d336d5f9a21102d6320e537_219_1.png)

![](img/a2132b646d336d5f9a21102d6320e537_220_0.png)

**Figure 7.7 Verify changes using winipcfg**

The output shows clearly that the DNS settings are *not* related to an individual IP address or network interface; they apply to the machine as a whole.

While it may seem strange not to configure the domain name (and hostname) yet, it does emphasize the functions of the various settings and clarifies how DNS operates, as we explained in Module 7.2. We will configure domain name and hostname in Module 8.14.

### Checking that it’s working

(This section is identical to the tests we ran for Linux in the previous module.)

Check that the DNS is working by **pinging** a host by name, or connecting to a site by name in your Web browser (or using any other application that uses hostnames).

> **Warning**: many Internet sites block **pings**. To be sure that DNS really is working, use **tcpdump** to see the DNS packets on the wire.

> **Warning**: if the **Domain** field is empty, Windows-NT will *not* use the DNS to resolve a simple name (i.e. one that doesn’t contain any dots, such as bob). However, that doesn’t matter as we are not using DNS internally, so all the names we want to resolve do contain dots (e.g. www.ibm.com) and resolve correctly. (See Chapter 8 Notes.)

> **Exercise 1**: run **tcpdump** (with option “**-n**”), **ping** the host www.debian.org (or any other machine on the Web) and see the DNS packets go out and in. Now **ping abcdef.** What do you see on the wire?

> **Exercise 2**: change your DNS configuration so that the first DNS server in the list doesn’t exist. (Use something like 10.10.10.123 or some other number from a private address set that you know isn’t in use on your network. Make sure it is not an address in your local segment’s range or you will only see failing ARPs.) Now try the **ping** again. Do you see any pattern in the intervals between successive DNS attempts? Now try two non-existent servers, and then all non-existent servers.

## 7.6 Lab – interrogating the DNS – nslookup and host

We said that the DNS client software isn’t a separate program – it’s built into every TCP/IP application. Even so, there are several special applications for checking out the operation of the DNS. These of course contain the resolver; in effect they are just a convenient front end to it. The two tools we’ll use are **nslookup** and **host**. Both are command-line programs without any GUI. We prefer **host** because it’s faster and easier to use; however, it’s available only for Linux (but see the Notes) whereas **nslookup** is standard on Windows too, so we’ll cover **nslookup** first.

> Tip: these commands are ideal as diagnostic tools for the DNS. When troubleshooting, we recommend you always run **tcpdump** too, to see *exactly* what’s happening.

You can run **nslookup** in two ways.

- 1. non-interactively: enter all the details of your DNS query on the command line. **nslookup** performs the query, prints the results, and exits:
  
  ```text
  alice% nslookup www.debian.org
  Server:	 n50.bt.net
  Address:	 194.72.6.51
  
  Name:	 www.debian.org
  Address:	 198.186.203.20
  alice%
  ```

- 2. interactively: enter the command name on its own, without any arguments. The program runs and gives you its own prompt. You enter a query, **nslookup** prints the result, and gives you its prompt again:
  
  ```text
  alice% nslookup
  Default Server:	 n50.bt.net
  Address:	 194.72.6.51
  > 
  ```

![](img/a2132b646d336d5f9a21102d6320e537_221_0.png)

Interactive mode is convenient if you have lots of queries to enter: you don’t have to type the command name each time, and you can set various parameters that persist from one query to the next. However, we’ve found it’s rarely necessary (especially as Linux shells and NT’s Command Prompt let you recall your previous command line and edit it) so we won’t deal with it any further here; see Appendix 11 if you need more information on it.

### Format of nslookup and host commands

The simplest command, which we used above, is:

```
`nslookup hostname`
```

**nslookup** prints the details of the DNS server it’s querying (it defaults to the one you specified in Control Panel > Network or /etc/resolv.conf) followed by the IP address corresponding to *hostname*, or an error message if it couldn’t resolve the name. The command `nslookup ipnumber`

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
