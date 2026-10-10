where *dns.companyname.com* should be replaced by the hostname of the caching nameserver. This points all DNS lookups of doubleclick.net to **127.0.0.1**, where they will not be found. To make the change effective, you have to restart *named* so that the new configuration information is read. Chapter 11 describes several different ways of restarting the *named* service; here is one of them:

```
# kill -HUP `pidof named`
```

When *named* is restarted, attempts to resolve all doubleclick.net addresses fail, the ads are neither loaded nor displayed, and your browsing experience is faster.

# # Your Own Domain Name and Third-Party DNS

It is possible to have your own domain name and provide third-party DNS service for it, meaning that you do not have to configure and administer a DNS nameserver for yourself. You can even have a mail address for your domain without having a mail server. Here is a summary of the major tasks involved in providing a third-party DNS service to your own domain name:

+   * **Register and pay for a unique domain name**—Several companies now offer to register these names, so shop around for the most reasonable price and perform some Google background checks on the company before using it.
+   * **Use a third-party DNS provider to provide DNS services**—One popular provider is ZoneEdit, which provides detailed steps to use the service. ZoneEdit also provides mail-forwarding services, so mail addressed to *you@yourown.domain* is forwarded to your regular ISP mail account. ZoneEdit also allows you to use Dynamic DNS, which enables you to run a server on a dynamically assigned IP (from a cable or dialup provider), yet still have DNS servers locate you. ZoneEdit can also provide a startup web page space for you or forward requests to an already established page with a long, complicated address.
+   * **Return to your domain name registrar and tell it what nameservers are authoritative for your domain.**

After you have completed the preceding tasks, it takes about three days for the information to propagate around the Internet.

# # Providing DNS for a Real Domain with BIND

BIND is the de facto standard DNS software suite for UNIX. It contains a nameserver daemon (*named*) that answers DNS queries, a resolver library that enables programs to make such queries, and some utility programs. BIND is maintained by the *ISC (Internet Software Consortium)* at the website http://www.isc.org/bind/.