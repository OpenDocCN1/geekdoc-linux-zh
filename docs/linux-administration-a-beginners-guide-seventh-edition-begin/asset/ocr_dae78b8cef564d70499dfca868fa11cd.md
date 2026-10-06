# Configuring CUPS

The main configuration file for the CUPS print daemon is cupsd.conf. It is usually located in the /etc/cups/ directory. It is a plain-text file with directives (syntax) similar to that of the Apache server. The variables used in the file determine how the server operates.

The file is well commented, and all that needs to be done is to uncomment certain lines in the file to turn functions on or off.
Here are some interesting directives used in the cupsd.conf file:

+   * Browsing Controls whether printer browsing is enabled. The options are Yes and No.

+   * BrowseLocalProtocol Specifies the protocols to use when collecting and distributing printer information on the local network. The options are all, none, and dnsmd.

+   * ServerName Specifies the hostname that is reported to clients. Typically, it's the same as the fully qualified hostname of the server.

+   * Listen Defines the address and port combination on which the CUPS daemon should listen.

+   * Allow Allows access from given addresses, hostnames, domains, or interfaces. This directive is valid only within the Location and Limit sections.

+   * Limit Specifies an operation or method to be limited in the Policy section of the configuration file.

+   * Location Specifies the access control rules for the given HTTP resource or file system path.

> NOTE The CUPS software is Internet Protocol version 6 (IPv6)–ready. To make the CUPS daemon listen on both IPv4 and IPv6 sockets, you could set the directive to something like Listen ::631. And if you need to configure a specific IPv6 address (such as 2001:db8::) explicitly for the CUPS server to listen on, you must enclose the IPv6 address in square brackets—for example, Listen [2001:db8::]:631.

A particularly interesting location is the root location, represented by the slash symbol (/). In the default cupsd.conf file looks like this (that line numbers have been added to the list to aid the discussion):

+   1. <Location />
2. Order allow, deny
3. Deny all
4. Allow localhost
5. </Location>