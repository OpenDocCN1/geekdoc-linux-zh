| Type | Description |
| :--- | :--- |
| **master** | Primary DNS zone |
| **slave** | Slave DNS server; controlled by a master DNS server |
| **hint** | Set of root DNS Internet servers |
| **forward** | Forwards any queries in it to other servers |
| **stub** | Like a slave zone, but holds only names of DNS servers |

**TABLE 36-4** DNS BIND Zone Types

Table 36-4 lists the BIND zone types. The following example shows a simple **zone** statement for the **mytrek.com** domain. Its class is Internet (in), and its type is master. The name of its zone file is usually the same as the zone name, in this case, **“mytrek.com.”**

```
zone "mytrek.com" in {
  type master;
  file "mytrek.com";
};
```

# Configuration Statements

Other statements, such as *acl*, *server*, *options*, and *logging*, enable you to configure different features for your name server (see Table 36-5). The **server** statement defines the

| Statement | Description |
| :--- | :--- |
| /* comment */ | BIND comment in C syntax. |
| // comment | BIND comment in C++ syntax. |
| # comment | BIND comment in Unix shell and Perl syntax. |
| acl | Defines a named IP address matching list. |
| include | Includes a file, interpreting it as part of the named.conf file. |
| key | Specifies key information for use in authentication and authorization. |
| logging | Specifies what the server logs and where the log messages are sent. |
| options | Global server configuration options and defaults for other statements. |
| controls | Declares control channels to be used by the ndc utility. |
| server | Sets certain configuration options for the specified server basis. |
| sortlists | Gives preference to specified networks according to a queries source. |
| trusted-keys | Defines DNSSEC keys preconfigured into the server and implicitly trusted. |
| zone | Defines a zone. |
| view | Defines a view. |

**TABLE 36-5** BIND Configuration Statements