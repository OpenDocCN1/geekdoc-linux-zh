When a BIND server has been configured as a forwarder, it automatically caches any answers it receives from the Internet DNS servers. No extra configuration is needed to enable this caching functionality.

When the forwards declaration is configured, start the nameserver with *rcnamed*:

```
bind:: # rcnamed start
Starting nameserver BIND 9
```

To automatically set named to start when you system boots, use *chkconfig* -a named.

Before you start testing the DNS server, you need to configure the DNS resolver. To do this, you need to edit the /etc/resolv.conf file. Change the nameserver entry to your newly created DNS server. In this case, this is 127.0.0.1.

```
search palmcoder.net
nameserver 127.0.0.1
```

When the DNS server is started, you can look up a host name on the Internet to check that the forwarder and DNS are working correctly. The *dig* program is used to query a DNS server for information (see Listing 21-1), and we use it throughout this chapter for this purpose.

# # Using dig

The dig program is being phased in as a replacement for the *nslookup application. With dig, you can query specific record types in a DNS zone. To query a specific record type, use the -t option. For example:

+   * To query the MX record of palmcoder.net, use *dig -t mx palmcoder.net.*
* For a nameserver (NS), use *dig -t ns palmcoder.net.*
* For an address record (A), use *dig -a www.palmcoder.net.*.

Listing 21-1: Using dig to Test a DNS Server

```
bind:: # dig www.palmcoder.net
;; Warning: ID mismatch: expected 23997, got 50172
;; Warning: ID mismatch: expected 23997, got 50172
<<>> DIG 9.2.3 << www.palmcoder.net
;; global options: printcmd
;; answer:
;;>>HEADER<< opcode: QUERY, status: NOERROR, id: 23997
;; flags: gr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 1, OPTIONAL: 0
```