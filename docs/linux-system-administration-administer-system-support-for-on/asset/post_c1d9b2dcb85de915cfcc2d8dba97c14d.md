
the application must decide how to send the data (which happens at the Transport Layer – in this case, TCP). Then, once it knows how to send the message, the application must decide where the data is going (which corresponds to the Network Layer – in this case, an IP address). The next vital bit of information is the physical address of the machine (known as the MAC address, which is on the Physical Layer). When the application knows all this, it sends the packet. The preparatory process that leads to this event is called *encapsulation*. When the packet is received, the whole elaborate ritual is reversed on the recipient’s side, a process called *de-encapsulation*.

In-between encapsulation and de-encapsulation, however, the two systems connected via TCP/IP must actually “talk to” each other.

## Understanding Network Addresses

The network address, or *IP address*, of each host consists of four sets of decimal numbers. The format looks like this:

aaa.bbb.ccc.ddd

Each three-digit number (represented here by `aaa` through `ddd`) can be a value from 0 to 256, totaling eight bits each. For example, my IP address might be (but isn’t really) 12.3.45.6. As long as you’re not connected to the Internet, you may choose any three-digit numbers you want. On the Net, however, certain numbers are not considered valid for addressing and are not used. Accordingly, when you establish your IP address, be sure you know beforehand how many networks – and how many hosts – you need.

## Network Classes

The designation of a network as Class A, Class B, or Class C reflects two characteristics: (1) the initial octet and (2) how it groups the addresses that correspond to `aaa`, `bbb`, `ccc`, and `ddd`. Table 11-3 compares the network classes in IP; side by side, they’re not hard to tell apart.

![](img/8ad518fddafc7f5e73715a2604b61d50_365_0.png)

> If you’re interested in learning more about network addressing and more detailed areas of networking, read *The LINUX Network*, by Fred Butzen and Christopher Hilton, IDG Books Worldwide, 1998.

TABLE 11-3 NETWORK CLASSES IN IP
| Class | Initial Octet | Network Addresses | Host Addresses |
| :--- | :--- | :--- | :--- |
| A | 1-126 | aaa | bbb.ccc.ddd |
| B | 128-191 | aaa.bbb | ccc.ddd |
| C | 192-224 | aaa.bbb.ccc | ddd |
| Reserved | 0, 127, 224-254* | n/a | n/a |

> *Zero is not used, and 127 is used for the loopback address. 224-254 is reserved for other network uses including broadcasting.*

As Table 11-3 illustrates, the numbers in the first part of a network address (the initial octet that corresponds to aaa) fall within a range that immediately reveals the network’s class. (Well, maybe not immediately, but certainly with practice.) So, quick quiz: Address 124.228.8.4 is in what class of network? (The answer is Class A.) The bad news is, this topic can get much more complex in a hurry; the good news is, not right now.

## Naming Your Networks with DNS

Most users don’t want to have to memorize numbers simply to get to another host on a network – and having to type numbers is almost as tedious for some. Instead of typing 128.227.8.4, for example, you could have typed maple.circa.ufl.edu. Such address names use the Domain Name Service (DNS) when you open a Web browser. For example, www.yahoo.com is the name that associates with any of several different IP addresses, depending on the network traffic.

The DNS naming convention works in a manner similar to that of the UNIX file-system structure. You begin with a root nameserver (.), and from there, decide whether the address you’re sending to is government (.gov), commercial (.com), nonprofit organization (.org), network service provider (.net), or part of another country. All these designations are called top-level domains. Table 11-4 lists top-level domains for countries.

TABLE 11-4 TOP-LEVEL DOMAINS FOR COUNTRIES

| Top-Level Domain | Country |
| :--- | :--- |
| .au | Australia |
| .ca | Canada |
| .cn | China |
| .de | Germany |
| .dk | Denmark |
| .eg | Egypt |
| .es | Spain |
| .fr | France |
| .it | Italy |
| .jp | Japan |
| .kr | Korea |
| .mx | Mexico |
| .ng | Nigeria |
| .no | Norway |
| .nz | New Zealand |
| .se | Sweden |
| .uk | United Kingdom |
| .us | United States (not used much) |
| .za | South Africa |

International top-level domains may not seem immediately relevant, but consider: They can be transparent to the user. Yahoo!, for example, may appear to be only one site when it's on your screen, but actually it's several. The Yahoo! Web site in the United States is www.yahoo.com; in France, it's www.yahoo.fr; in Germany, it's www.yahoo.de. Such behind-the-scenes information can be useful to an administrator.

When a DNS client looks up a name such as `corp.hp.com`, the process is much more tortuous than it seems. First your client goes to the current DNS table. If your DNS address is `maple.circa.ufl.edu`, for example, the client looks in the table for `circa.ufl.edu`. It doesn’t find anything, so it goes up to `ufl.edu` – still nothing. Next, it goes up to `.edu` and looks there. Again nothing. Now it goes to the root domain, `.`, and finds `.com`. Now that it’s found `.com`, it looks for `hp.com`. Found it. Now down to `corp.hp.com`. Because the client has done all that work, we know that `corp.hp.com` exists – so we don’t have to type in the IP address.

These domains can have other domains in them or go directly to a host (`www.ins.com` is a host where `corp.sun.com` is a domain). It’s all a matter of how the domain is structured. For `tigerlair.com`, it’s fairly easy. There are two hosts that are recognized: `www.tigerlair.com` and `ftp.tigerlair.com`. There are no subdomains like `corp.tigerlair.com` (for functionality division) or `florida.tigerlair.com` (for regional division).

## LINUX DNS CLIENT

To make your Linux host a DNS client, all you have to do is define a nameserver and create an `/etc/resolv.conf` file. One may look like this:

```text
domain best.com
nameserver 152.52.2.2
```

This defines your domain and the IP address of the nameserver. Instead of looking in the `/etc/hosts` file, Linux will query the nameserver for the information. Your DNS client configurations are done through `/sbin/netconfig`. If you want to test a nameserver query, run `nslookup`. If you are using DNS, you can keep a minimal sized `/etc/hosts` file, with one line containing the localhost address.

```text
Server: localhost
Address: 127.0.0.1

Non-authoritative answer:
Name: www9.yahoo.com
Address: 204.71.200.74
Aliases: www.yahoo.com
```

## LINUX NAMESERVER

You can set up your Linux server as a nameserver as well. For example, I have the domain `tigerlair.com`. If I wanted to set up subdomains like `tchedn` and `kitchen` or hosts like `tiger` or `sharekahn`, I would have to set up a host to be the authority on what names are actually in the `tigerlair.com` domain. In other words, the nameserver provides official information about the hosts and subdomains in `tigerlair.com`.

To set up Linux as a nameserver, you would have to install the package `bind`, which is the UNIX implementation of DNS. The current version of BIND is 8; be sure to keep BIND up to date for bug fixes and security patches. To configure the nameserver, you would edit the /etc/named.conf file to meet your needs. Here is an example one for tigerlair.com:

```text
/*
 * BIND 8 configuration for faux tigerlair.com
 * This shows a basic BIND 8 config file.
 */

options {
	directory "/var/named";
};
```

This sets your directory for your configuration files that are defined as follows:

```text
logging {
	category lame-servers { null; };
	category cname { thelair; };
};
```

This enables logging, including any conical names (aliases) for the domain.

```text
zone "tigerlair.com" in {
	type master;
	file "tigerlair.hosts";
};
```

The listing above defines this nameserver as master server. If the master server goes down, the slave server takes the requests. You would not define both the slave and the master server as the same host.

```text
zone "0.23.12.in-addr.arpa" in {
	type master;
	file "tigerlair.rev";
};
```

The listing above defines this nameserver as master server for the network 12.23.0.0. This means it will translate any name on that network to the correct address.

```text
zone "tigerlair.com" in {
	type slave;
	file "tigerlair-slave.hosts";
	masters { 12.23.10.1; };
};
```
