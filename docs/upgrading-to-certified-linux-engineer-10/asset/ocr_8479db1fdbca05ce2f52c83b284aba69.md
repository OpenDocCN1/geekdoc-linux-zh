In the following table, the most important record types are listed:

# Table 9-2

| Record Type | Meaning | Value |
|---|---|---|
| SOA | Start of Authority | Parameter for the domain |
| NS | DNS server | Name of a DNS server for this domain |
| MX | Mail exchanger | Name and priority of a mail server for this domain |
| A | Address | IP address of the computer |
| PTR | Pointer | Name of the computer |
| CNAME | Canonical name | Alias name for the computer |

Alternatively, you can specify a file containing the needed commands. An ASCII file (called updates) with the following content delivers the same result as the interactive DNS update as shown above:

```
da51:~# cat updates
update delete da7.digitalairlines.com
update add da8.digitalairlines.com 84600 A 10.0.0.8
da51:~# nsupdate -v -k dhcp-dns.+157+23165.key updates
da51:~#
```