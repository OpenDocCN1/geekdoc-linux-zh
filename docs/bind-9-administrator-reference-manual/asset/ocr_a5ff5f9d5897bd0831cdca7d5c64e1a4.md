```
dig [@server] domain
[query-type][query-class][+query-option][-dig-option][%comment]
```

The usual use of dig will take the form
dig @server domain query-type query-class

For more information and a list of available commands and options, see the dig man page.

host

The host utility provides a simple DNS lookup using a command-line interface for looking up Internet hostnames. By default, the utility converts between host names and Internet addresses, but its functionality is extended with the use of options.

```
host [-acdRTvw] [-c class] [-N ndots] [-t type] [-W timeout] [-R retries] hostname
[server]
```

For more information and a list of available commands and options, see the host man page.

# nslookup

nslookup is a program used to query Internet nameservers. nslookup has two modes: interactive and non-interactive. Interactive mode allows the user to query nameservers for information about various hosts and domains or to print a list of hosts in a domain. Non-interactive mode is used to just print the name and requested information for a host or domain.

```
nslookup [option...][host-to-find] - [server]
```

Interactive mode is entered when no arguments are given (the default nameserver will be used) or when the first argument is a hyphen ('-') and the second argument is the host name or Internet address of a nameserver.

Non-interactive mode is used when the name or Internet address of the host to be looked up is as the first argument. The optional second argument specifies the host name or address of a nameserver.

Due to its arcane user interface and frequently inconsistent behavior, we do not recommend the use of nslookup. Use dig instead.