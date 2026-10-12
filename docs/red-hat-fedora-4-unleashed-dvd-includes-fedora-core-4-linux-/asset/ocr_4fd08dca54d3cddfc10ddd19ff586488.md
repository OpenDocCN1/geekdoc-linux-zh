```
options {      ...
blackhole {       203.122.154.1;      };
}
```

For a known source of bad data, you can do something such as the following to cause your nameserver to stop asking the listed server any questions. This is different from adding a host to the black hole list. A server marked as bogus will never be sent queries, but it can still ask us questions. A black holed host is simply ignored altogether:

```
server bogus.info.example.com {    bogus yes;};
```

The AUS-CERT advisory AL-1999.004, which discusses denial of service attacks against DNS servers, also discusses various ways of restricting access to nameservers and is a highly recommended read. A copy is located at ftp://ftp.auscert.org.au/pub/auscert/_advisory/AL-1999.004.dns_dos. Among other things, it recommends the most restrictive configuration possible and the permanent black-holing of some addresses known to be popular sources of spoofed requests and answers. It is a good idea to add the following ACL to the black hole list of all your servers:

```
/* These are known fake source addresses. */
acl "bogan" {
    0.0.0.0/8;       # Null address
    1.0.0.0/8;       # IANA reserved, popular fakes
    2.0.0.0/8;       192.0.2.0/24; # Test address
    224.0.0.0/3;     # Multicast addresses

    /* RFC 1918 addresses may be fake too. Don't list these if you
       use them internally. */
    10.0.0.0/8;
    172.16.0.0/12;
    192.168.0.0/16;
};
```

# ## Using DNS Security Extensions

DNS Security Extensions (DNSSEC), a set of security extensions to the DNS protocol, provides data integrity and authentication by using cryptographic digital signatures. It provides for the storage of public keys in the DNS and their use for verifying transactions. DNSSEC still isn't widely deployed, but BIND 9 does support it for inter-server transactions (zone transfers, NOTIFY, recursive queries, dynamic updates). It is worth configuring