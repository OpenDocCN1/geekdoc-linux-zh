
Such as `edu` (for colleges and universities), `gov` (for United States government), and `mil` (for United States military sites) were among the most used TLDs in the early Internet. In more recent years, `com` (for commercial sites) has experienced the most growth.

The `us` domain was added to include U.S. institutions, such as local governments and elementary schools, as well as to individuals within a geographical region of the United States. Recently, new domains such as `info` (for people and business to publish information about themselves) and `biz` (an alternative to `com` for businesses) have been added.

To facilitate the entry of other countries to the Internet, the International Organization for Standardization (ISO) has defined a set of two-letter codes that are assigned to each country. Within each country are naming authorities responsible for organizing the subdomains. Some subdomains are organized by categories, while others are structured by geographic location.

> **TIP:** Several RFCs (Request for Comments) define the domain name system. RFC 1034 covers domain name concepts and facilities. RFC 1035 is a technical description of how DNS works. RFC 1480 describes the `us` domain. For a more general description of DNS, there is RFC 1591. You can view RFCs at the RFC Database (`www.rfc-editor.org/rfc.html`).

## Common top-level domain names

Of the generic TLDs in use today, several are used throughout the world, while two are available only in the United States. Here are descriptions of common TLDs:

- **com** — Businesses, corporations, and other commercial organizations fall into this TLD. As the Internet has grown into an important tool for commerce, domains in this TLD have grown at a dramatic rate.
- **edu** — Colleges and universities fall under this TLD. Although it was originally intended for all educational institutions, two-year colleges, high schools, and elementary schools are now organized by location under country codes (such as US in the United States).
- **gov** — This TLD is used primarily for U.S. federal government locations. Although most local government sites are expected to fall under the `us` domain, some states (including Washington state) are making the `gov` TLD available to local cities and counties.
- **int** — This domain includes international databases and organizations created by international treaties such as NATO.
- **mil** — U.S. military organizations fall under this domain.
- **net** — Computer network providers fall under this domain.
- **org** — A variety of organizations that are neither governmental nor commercial in nature fall under this catchall TLD.

As noted earlier, other TLDs have been added recently to relieve some of the drain on `.com` names. In particular, those doing business on the Internet can get a `.biz` name. If you want to create a gathering point for information on a subject, you might choose a domain name from the `.info` TLD.

## Domain-name formation

As noted earlier, domain names are hierarchical, which means there can be subdomains beneath second-level domains, as well as host computers. (Second-level domains are the names directly below the TLDs that are assigned to individual people and organizations.) Each subdomain is separated by a dot (.), starting with the top-level domain on the right and with the second-level domain and each subsequent subdomain appearing to the left. Here is an example of a fully qualified domain name for a host:

```
baskets.crafts.hansonhistory.com
```

In this example, the top-level domain is `.com`. The second-level domain name assigned to the organization that controls the domain is `hansonhistory`. Within that domain is a subdomain, or third-level domain, called `crafts`. The last name (`baskets`) refers to a particular computer within that third-level domain. From other hosts in the third-level domain, the host can be referred to simply as `baskets.crafts`. From the Internet, you would refer to it as `baskets.crafts.hansonhistory.com`.

> CROSS-REFERENCE: For more details on how the domain-name system is structured, and for information on how to set up your own DNS server in Fedora, see Chapter 25.

## Host names and IP addresses

In the early days of the Internet, every known host computer name and address was collected into a file called HOSTS.TXT and distributed throughout the Internet. This quickly became cumbersome because of the size of the list and the constant changes being made to it. The solution was to distribute the responsibility for resolving host names into IP addresses to many DNS servers throughout the Internet.

To make the domain names friendly, the names contain no network addresses, routes, or other information needed to deliver messages. Instead, each computer must rely on some method to translate domain names and host names into IP addresses. The DNS server is the primary means of resolving the names to addresses. If you request a service from a computer using a fully qualified domain name (including all domains and subdomains), the request will go to a DNS server to resolve that name into an IP address. It will gather that information either directly from the DNS server that owns that information or, which is more likely, from another DNS server along the way that has gathered that information.

If you have a private LAN or other network, you can keep your own list of host names and IP addresses. For the computers you work with all the time, it’s easier to type `baskets` than `baskets.crafts.hansonhistory.com`. There are a couple of ways (besides DNS) that your computer can resolve the IP address for computers for which you give only the host name:

- **Check the `/etc/hosts` file.** In your computer's `/etc/hosts` file, you can place the names and IP addresses for the computers on your local network. In this way, your computer doesn't need to query the DNS server to get the address (which may not be there anyway if you are on a private network and don't have your own DNS server).
- **Check specified domains.** You can specify that if the host name requested doesn't include a fully qualified domain name and the host name is not in your `/etc/hosts` file, then your computer should check certain specified domain names.

On your Fedora system, when you make a request to resolve a host name into an IP address, the contents of the `/etc/resolv.conf` file will most likely determine where your computer searches for that information. That file can specify your local domain, an alternate list of domains, and the location of one or more DNS servers. Here is an example of an `/etc/resolv.conf` file:

```
domain crafts.hansonhistory.com
search crafts.hansonhistory.com hansonhistory.com
nameserver 10.0.0.10
nameserver 10.0.0.12
```

In this example, the local domain is `crafts.hansonhistory.com`. If you try to contact a host by giving only its host name (with no domain name), your computer can check in both `crafts.hansonhistory.com` and `hansonhistory.com` domains to find the host. If you give the fully qualified domain name, it can contact the name servers (first 10.0.0.10 and then 10.0.0.12) to resolve the address. (You can specify up to six name servers that your computer will query in order until the address is resolved. The total search line is limited to 256 characters, however.)

If your system uses DHCP, where another server on your network assigns your Linux system an IP address, your `/etc/resolv.conf` file can look more like the following:

```
; generated by /sbin/dhclient-script
search ccl2.client2.big_esp.com
nameserver 10.0.0.10
nameserver 10.0.0.12
```

In this example, the `/etc/resolv.conf` file was created by the DHCP client code, based on information from the DHCP server. Note that `big_esp.com` is an alias for a large communications company.

> TIP: Your resolver knows to check your `/etc/hosts` file first because of the contents of the `/etc/host.conf` and `/etc/nsswitch.conf` files. By default, the `nsswitch.conf` file has your resolver check local files first, followed by DNS to resolve addresses. The `host.conf` file indicates that local files (hosts) be checked first for the address, followed by the DNS system (bind). You can change that behavior by modifying those files. See the `resolv.conf` man page for further information.

## Routing

Knowing the IP address of the computer you want to reach is one thing; being able to reach that IP address is another. Even if you connect your computers on a LAN, to have full connectivity to the Internet there must be at least one node (that is, a computer or dedicated device) through which you can route messages that are destined for locations outside your LAN. That is the job of a *router*.

A router is a device that has interfaces to at least two networks and is able to route network traffic between the two networks. In my example of a small business that has a LAN that it wants to connect to the Internet, the router would have a connection and IP address on the LAN, as well as a connection and IP address to a network that provides access to the Internet.

A computer running Linux can act as a router between any two TCP/IP interfaces, for example, if the computer has two LAN cards or if it has a network interface card and a modem (for a dial-up connection to the Internet). Alternatively, you can purchase a dedicated router, such as Cisco ADSL routers, that can exclusively perform routing between your LAN and the Internet or network service provider.

> TIP: Unlike regular dial-up modems, xDSL routers or bridges have several different standards that are not all compatible. Before purchasing an xDSL modem, check with your ISP. If your ISP supports xDSL, it can tell you the exact models of xDSL modems you can use to get xDSL service.

## Proxies

Instead of having direct access to the Internet (as you do with routing), you can have indirect access via the computers on your LAN by setting up a *proxy server*. With a proxy server, you don’t have to configure and secure every computer on the LAN for Internet access. When, for example, a client computer tries to access the Internet from a Web browser, the request goes to the proxy server. The proxy server then makes that request to the Internet. Using a proxy server, Internet access is fairly easy to set up and quite secure to use. Fedora can be configured as a proxy server (as described later in this chapter).

## Using Dial-up Connections to the Internet

Many individuals and even some small businesses that need to connect to the Internet still do so using modems and telephone lines. Your modem connects to a serial port (COM1, COM2,
