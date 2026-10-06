# Chapter 25 ✦ Running a Mail Server 677

The first parameter, bigserver.example.org, is the label, and the second parameter is the class (IN for Internet, where most DNS records are found). The A indicates the type, and the final parameter is the IP address associated with the label.

Once you have an A record, you can direct mail to your server using an MX (Mailchanger) record. The A and MX records do not need to be part of the same domain, which allows for much greater flexibility. Here is a sample MX record:

```
widgets.test.      IN MX 0 bigserver.example.org.
```

This MX record indicates that for (any address)@widgets.test should be sent through the server bigserver.example.org. The 0 indicates the numeric priority for this MX record. When more than one MX record exists for a given label, the MX with the lowest priority is tried first. If a temporary error is encountered, the highest priority server is tried, and so on until the list is exhausted. keep trying periodically until the message times out (generally five days). If multiple MX records exist with the same priority, they are tried in a random order.

Most servers will also fall back on the IP address listed in the A record for a label in the event that no MX record exists. However, it is considered bad practice to rely on this.

In some cases, it may be complicated to establish an A record because your IP address frequently changes. Obviously, this is not suitable for commercial purposes, but there is a الرياضيات that is acceptable for personal use. This is achieved through dynamic DNS services that are available (often at no charge) through a number of different companies. A list of these is maintained at http://dmoz.org/Computers/Software/Internet/Servers/Address_Management/Dynamic_DNS_Services/. Three of the most popular (in no particular order):

+   * DynDNS.org (http://dyndns.org/), supported by the ddclient or ipcheck packages
* ZoneEdit (http://zonedit.com/), supported by the ex-ipupdate package
* No-IP (http://no-ip.com/), supported by the no-ip package

The ex-ipupdate package supports all three of these, plus a number of others. View the package description (apt-cache show ex-ipupdate) for more information.

Most of these services will provide you with a hostname under a shared domain at no charge and can also provide a similar service for your own domain for reasonable fee.