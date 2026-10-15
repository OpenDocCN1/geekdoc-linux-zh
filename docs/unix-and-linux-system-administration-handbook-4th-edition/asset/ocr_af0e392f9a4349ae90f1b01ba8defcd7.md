Since DNS uses UDP for queries and since DNS responses are often larger than 512 bytes, DNS administrators have to worry about large UDP packets being dropped. If a large reply gets fragmented and your firewall only lets the first fragment through, the receiver gets a truncated answer and retries the query with TCP. TCP is much more expensive, and busy servers at the root or TLDs don’t need increased TCP traffic because of everybody’s broken firewalls.

The edns-udp-size option sets the reassembly buffer size that the name server advertises through EDNS0, the extended DNS protocol. The max-udp-size option sets the maximum packet size that the server will actually send. Both sizes are in bytes. Reasonable values are in the 512–4,096 byte range.

Both values default to 4,096 bytes to help accommodate new features such as DNSSEC, IPv6, and internationalized domain names. However, some (broken) firewalls do not allow UDP packets larger than 512 bytes, and others are configured to block all but the first packet of a fragmented UDP response. The only real solution is to fix the firewalls.

To get an idea of what packet size is OK for your site, try running the command dig rs.dns-oarc.net txt and see what comes back; see page 652 for more details about the DNS-OARC reply-size server. If this tool shows a small size, the problem is probably at your perimeter and you will need to fix your firewalls.

As an interim solution, try setting the max-udp-size parameter to the value shown by the reply-size server. This setting makes named squeeze its answers into packets that might get through unfragmented. Set edns-udp-size to the same value so that you can get packets flowing in both directions. Don’t forget to set the values back to 4,096 after you fix your firewalls!

Avoid these options unless you are sure you have a packet size problem, since they also limit the size of packets along paths that can handle a full 4,096 bytes.

```
dnssec-enable yes | no; [yes]
dnssec-validation yes | no; [yes]
dnssec-lookaside domain trust-anchor domain; ["", "dlv.isc.org"]
dnssec-must-be-secure domain yes | no; [none]
```

These options configure support for DNSSEC. See the sections starting on page 648 for a general discussion of DNSSEC and a detailed description of how to set up DNSSEC at your site.

An authoritative server needs the dnssec-enable option turned on. A recursive server needs the dnssec-enable and dnssec-validation options turned on and a trust anchor specified with a trusted-keys statement.

If there is no trust anchor for the domain in question, the software tries to find one by using the dnssec-lookaside option, which skirts the issue of the parent domains not using DNSSEC.