
So please don't try to use them.) Behind the DNS server (which is also operating as a firewall) are four client computers that have private IP addresses. (You can reuse these addresses and other private addresses that I describe in Chapter 15.)

**Note:** Because this is an example of how DNS works, it doesn't deal with all the complexities you might face in setting up the computing infrastructure at your company. For example, you might well want a dedicated firewall protecting your Internet connection, with the DNS server being placed with the other servers behind what is referred to as a **demilitarized zone** that is separated from the company LAN.

![](img/fb202c163797a743c3c6cf236316bc96_998_0.png)

The job of the DNS server, in this configuration, is to map the names of the public servers (`www.yourdomain.com`, `mail.yourdomain.com`, `ftp.yourdomain.com`, and `ns1.yourdomain.com`) into the static IP addresses that the ISP assigns (`123.45.67.1`, `123.45.67.2`, `123.45.67.3`, and `123.45.67.89`, for our example). The DNS server also provides DNS service from the private addresses on the LAN, so each computer can reach the others on the LAN without needing to store all computer names in their own `/etc/hosts` file.

A key feature to this example is that it divides the view of this domain between what the outside world can see and what the computers on the private network can see. Using the `view` feature of BIND, I create an *outside* view that lets queries from the Internet find only public servers (Web, Mail, and FTP) in the domain. Then I create an *inside* view that lets queries from the local LAN find both the public servers and private computers (red, blue, green and yellow) in the domain.

The sections that follow describe how to set up a DNS server for the example in Figure 25-1.

## Quick-starting a DNS server

The DNS server software that comes with the current Fedora and RHEL versions is Berkeley Internet Name Domain (BIND) version 9. To configure BIND 9, you work with the following components:

- **Configuration file** (`/var/named/chroot/etc/named.conf`)— The main DNS server configuration file.
- **Zone directory** (`/var/named/chroot/var/named`)— The directory containing files that keep information about Internet root DNS servers (`named.ca` file) and information about the zones that you create for your DNS server.
- **Daemon process** (`/usr/sbin/named`)— The daemon process that listens for DNS requests and responds with information that the `named.conf` file presents.
- **Debugging tools** (`named-checkconf`, `named-checkzone`)— What you use to determine whether you created your DNS configuration correctly.

**Note:** Fedora and RHEL come with a GUI tool for configuring BIND called `system-config-bind`. (Type `yum install system-config-bind` to install it.) If you decide to use that tool, you need to be careful editing the BIND configuration files by hand. It is recommended that if there are changes you want to make to the `named.conf` file that are not supported by the `system-config-bind` window, you should put those changes in the `/etc/named.custom` file instead.

BIND 9 also includes tools for creating DNSSEC secured zones. By using these tools, you can create and generate keys to provide authentication and secure address resolution. The example illustrated in these sections doesn’t include DNSSEC configuration.

The basic steps in creating a DNS server for your example are as follows:

- Identifying your DNS servers
- Creating DNS configuration files (`named.conf` file and the `named` directory)
- Starting the named daemon
- Monitoring named activities

In the example configuration, you set up a primary master DNS server and a slave DNS server. The primary server holds the master copy of the authoritative records for the domain. The secondary server is there to share requests for information about the domain, particularly in case the primary goes down. The secondary typically gets its records from the primary server. The secondary is also considered to be authoritative in regards to the DNS records for the domains it controls.

## Identifying your DNS servers

If you didn't have your DNS servers set up at the time that you purchased your domain name with a registration authority, you might have just "parked" the domain name there until you configured your DNS servers. Whenever you're ready to set up your DNS servers, return to that registration authority and provide the following information about your DNS servers:

- DNS server IP addresses (the static IP addresses of your DNS servers, probably primary and slave)
- DNS server hostnames (often `ns1.yourdomain.com`, where you replace `yourdomain.com` with your domain name for the primary; the slave hostname is `ns2.yourdomain.com`)

You should register both the primary and slave DNS servers. After you update this record, that information typically takes a day or two to propagate throughout the Internet. When your DNS servers are registered, you also need to tell the registration authority to use those DNS servers as the authority for addresses in your domain. The registration authority probably offers an online form you can fill out to identify your DNS servers.

## Creating DNS configuration files (named.conf and var/named)

In configuring a DNS server, you're actually creating definitions that apply to a particular *zone* in the public DNS tree, as well as several local zones that apply to your computer and local network. To create a useful DNS server for your example small-office environment, you have the following zones:

- **Public DNS server zone**— The DNS server is authoritative for the domain that you're serving. This zone serves the names and IP addresses for your public servers. In the example `named.conf` file shown in the next section, you need to replace the name `yourdomain.com` with the domain that you're creating. These records become accessible to everyone on the Internet.
- **Private DNS server zone**— So each computer on the private network doesn't need to know the IP addresses for other computers on your private network, a zone is added in the example `named.conf` file to let the DNS server resolve these addresses. The names and IP addresses (which are private) are available only to computers on your LAN.

Note that by creating different views of these zones, different information will be returned to queries, depending on where the queries come from. For example, when someone from the Internet requests the address of the DNS server (`ns1.yourdomain.com`), they will get the address 123.45.67.89. However, when a query for `ns1.yourdomain.com` comes from inside the LAN, the address 10.0.0.1 is returned. Also, any queries from the Internet for addresses of private computers (`red.yourdomain.com`, `blue.yourdomain.com`, and so on) are rejected.

## Editing named.conf

To begin, you configure the `/var/named/chroot/etc/named.conf` file on the primary master DNS server representing your example `yourdomain.com` domain. This example starts from the `/etc/named.conf` file that comes with the caching-nameserver package in Fedora and RHEL. (Make sure that you install the caching-nameserver and bind packages before you continue and make a backup copy of any configuration files you edit.) Following are a few tips relating to editing the `named.conf` file:

- If a statement contains substatements, make sure that you end the last substatement with a semicolon.
- Comments can appear in the same formats that popular programming languages use. These languages include C (begin with `/*` and end with `*/`), C++ (begin with `//` and go to the end of the physical line), and shell or Perl styles (begin from a `#` and go to the end of the physical line).
- A leading exclamation mark (`!`) negates an element. Putting `!123.45.67.89` in a statement causes the IP address `123.45.67.89` not to match the element. (Just make sure that the negation occurs before a positive match or the positive match takes precedence.)

The edited version of the `/var/named/chroot/etc/named.conf` file is as follows:

```
options {
    directory "/var/named";
    dump-file "/var/named/data/cache_dump.db";
    statistics-file "/var/named/data/named_stats.txt";
};

acl "mylan" {
    127/8; 10.0.0.0/24;
};

controls {
    inet 127.0.0.1 allow { localhost; } keys { rndckey; };
};

view "inside" {
    match-clients { "mylan"; };
    recursion yes;

    zone "." IN {
        type hint;
        file "named.ca";
    };

    zone "0.0.10.in-addr.arpa" IN {
        type master;
        file "yourlan.db";
```
