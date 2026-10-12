# **ARGUMENTS**

The first argument is normally the host name (domain name) for which you want to look up the requested information. If the first argument is an Internet address, a query is done on the special “reverse mapping” domain to look up its associated host name.

If the -l option is given, the first argument is a domain zone name for which a complete listing is given. The program enters a special zone listing mode, which has several variants.

The second argument is optional. It allows you to specify a particular server to query. If you don’t specify this argument, default servers are used, as defined by the /etc/resolv.conf file.

# **EXTENDED SYNTAX**

If the -x option is given, it extends the syntax in the sense that multiple arguments are allowed on the command line. An optional explicit server must now be specified using the -X option as it cannot be given as an ordinary argument any more. The -X option implies -x.

The extended syntax allows no arguments at all, in which case the arguments will be read from standard input. This can be a pipe, redirection from a file, or an interactive terminal. Note that these arguments are the names to be queried, and not command options. Everything that appears after a “#” or “;” on an input line will be skipped. Multiple arguments per line are allowed.

# **COMMONLY USED OPTIONS**

- **-v** list information in “verbose” format. (Without this option, the ttl and class fields are not shown.) Also the contents of the “additional information” and “authoritative nameservers” sections in the answer from the nameserver are printed, if present. Normally these sections are not shown.

- **-vv** very verbose

- **-t** querytype: allows you to specify a particular type of resource record information to be looked up. Supported types are listed below. The wildcard may be written as either ANY or *. Types may be given in upper or lower case. The default is type A for regular lookups, and A, NS, and PTR for zone listings.

- **-a** is equivalent to -t ANY. Note that this gives you “anything available” (currently cached) and not “all defined data” if a non-authoritative server is queried.

# **SPECIAL MODES**

The following options put the program in a special mode:

- **-l** zone: generates the listing of an entire zone.

- **-A** enters a special address check mode.