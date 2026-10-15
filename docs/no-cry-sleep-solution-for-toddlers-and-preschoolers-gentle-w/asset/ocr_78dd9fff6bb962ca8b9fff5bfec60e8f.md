# DNS Documentation

Currently, ISC has contracted with two companies, Nominum and Mind, to provide BIND support. Nominum is an ISC support partner and has taken an active role in BIND development. At its Web site at www.nominum.com, you can find BIND documentation, including the BIND 9 Administrator’s Reference. Nominum, like many commercial companies that support open source software, provides professional consultant and support services, while freely contributing to Open Source development. Mind provides consulting services for the European market.

# BIND Servers and Tools

The BIND DNS server software consists of a name server daemon, several sample configuration files, and resolver libraries. As of 1998, a new version of BIND, beginning with the series number 8.x, implemented a new configuration file using a new syntax. Version 9.0 adds new security features and support for IPv6. Older versions, which begin with the number 4.x, use a different configuration file with an older syntax. Most distributions currently install the newer 9.x version of BIND.

The name of the BIND name server daemon is named. To operate your machine as a name server, simply run the named daemon with the appropriate configuration. The named daemon listens for resolution requests and provides the correct IP address for the requested hostname. You can use the Remote Name Daemon Controller utility, rndc, provided with BIND to start, stop, restart, and check the status of the server as you test its configuration. rndc with the stop command stops named and, with the start command, starts it again, reading your named.conf file. rndc with the help command provides a list of all rndc commands. See the Red Hat Reference Guide for detailed information on configuring rndc access to your DNS server. Once your name server is running, you can test it using the dig or nslookup utility, which queries a name server, providing information about hosts and domains. If you start dig with no arguments, it enters an interactive mode where you can issue different dig commands to refine your queries. Numerous other DNS tools are also available, such as nslnt and host. Check the DNS Resource Directory at www.dns.net/dnsrd for a listing. Table 34-3 lists several DNS administrative tools.

| Tool | Description |
|---|---|
| dig domain | Domain Information Groper, tool to obtain information on a DNS server. Preferred over nslookup. |
| host hostname | Simple lookup of hosts. |
| nslookup domain | Tool to query DNS servers for information about domains and hosts. |
| rndc command | Remote Name Daemon Controller, an administrative tool for managing a DNS server (version 9.x). |
| ndc | Name Daemon Controller (version 8.x). |
| redhat-config-bind | Red Hat Bind DNS server configuration tool. |