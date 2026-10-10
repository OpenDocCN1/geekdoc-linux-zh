+   - `/usr/share/doc/bind-9*/arm` — Contains HTML and XML versions of the BIND 9 Administrator Reference Manual.
+   - **Man pages** — Type the `man` command, following it with `named` or `named.conf`. These man pages contain terse descriptions of options and variables that relate to the `named` daemon and `named.conf` file, respectively.
+   - **Internet Software Consortium** (www.isc.org/sw/bind) — The ISC Web site contains information and downloads related to BIND. On this site, find links to BIND mailing lists, security advisories relating to BIND, and BIND history.

# Summary

The choice to connect your Fedora or Red Hat Enterprise Linux server to the Internet isn’t one to make lightly. If the server is critical to your business and support for the server is too much for you to handle, you should consider handing your server over to a hosting provider.

If you do decide to expose your Fedora or Red Hat Enterprise Linux server to the Internet to offer Web, FTP, mail, or other types of services, you should carefully consider the security implications and prepare for them. By using Linux features that I describe in other parts of this book, you can create firewalls, monitor log files, and track changes to system files to protect your computers.

One way of controlling the public exposure of your servers is to obtain a domain name and configure your own Domain Name System (DNS) server. You can set up your DNS server to resolve hostnames to IP addresses for clients that request the information from the Internet, as well as to the users on your local, private LAN.