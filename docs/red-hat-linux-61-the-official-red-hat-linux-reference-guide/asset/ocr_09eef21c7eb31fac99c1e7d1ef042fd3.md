# Chapter 12. Berkeley Internet Name Domain (BIND)

# 12.6. Common Mistakes to Avoid

It is very common for beginners to make mistakes when editing BIND configuration files. Be sure to avoid the following issues:

+   - Take care to increment the serial number
- If the serial number is not incremented, the master nameserver may have the correct, new information, but the slave nameservers will never be notified of the change or attempt to refresh their data of that zone.
- Be careful to use ellipses and semi-colons correctly in the `/etc/named.conf` file. An omitted semicolon or unexpected ellipse will cause named to refuse to start.
- Remember to use periods (.) in zone files after all FDNs and omit them on hostnames.
- A period at the end of a domain name denotes a fully qualified name. If the period is omitted, named adds the name of the zone or the `$ORIGIN` value to complete it.
- If a firewall is blocking connections from the named program to edit its configuration file.
By default, BIND version 9 uses random ports over 1024 to query other nameservers. Firewalls, expect all nameservers to communicate using only port 53. Force named to use port 53 by adding the following line to the options statement of `/etc/named.conf`: `query-source-address * port 53;

# 12.7. Additional Resources

The following sources of information will provide additional resources regarding BIND.

# 12.7.1 Installed Documentation

+   - BIND features a full-range of installation documentation covering many different topics, each placed in its subject directory:
- `/usr/share/doc/bind-<version-number>/` — Contains a README file with the list of the most recent features.
- `/usr/share/doc/bind-<version-number>/arm/` — Contains HTML and SGML of the BIND 9 Administrator Reference Manual, which details BIND resource requirements, how to configure different types of nameservers, perform load balancing, and other topics. For most users of BIND, this is the best place to start.
- `/usr/share/doc/bind-<version-number>/draft/` — Contains assorted documents that reviews issues related to DNS service and methods proposed to address them.
- `/usr/share/doc/bind-<version-number>/misc/` — Contains documents designed to address specific advanced issues. Users of BIND version 8 should consult the migration document for options they must make when moving to BIND 9. The options file lists all the options implemented in BIND 9 that are used in `/etc/named.conf`.
- `/usr/share/doc/bind-<version-number>/rfc/` — Every RFC document related to BIND is in this directory.
- man named — Explores aspects that can be used to control the BIND nameserver daemon.