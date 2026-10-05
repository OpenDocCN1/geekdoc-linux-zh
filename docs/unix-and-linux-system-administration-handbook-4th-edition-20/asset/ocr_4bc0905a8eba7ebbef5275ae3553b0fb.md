# What's new in DNS

maintained BIND since version 4. The BIND 10 effort has been funded by sponsoring organizations around the world, mostly domain registrars.

BIND 10 will continue to be an open source reference implementation of DNS. It will be partially built by BIND 9 and will focus on improving modularity, custom-izability, clusterization, integration, resilience, and run-time control.

BIND 9 and earlier versions stored the BIND database in memory; BIND 10 will support multiple data storage systems. Another planned feature is a user interface API so folks can build GUI interfaces to populate zones and control the software. see isc.org/bind10 for details.

Several of other “what's new” issues from previous editions are still in the proposed-standard-but-not-yet-widely-adopted pile. Some examples are DNS-sec(security), IDN (internationalized domain names), and IPv6. These initiatives are progressing, but slowly. We include them at the end of Table 17.4, which lists many topics, relevant RFCs, and references to the pages in this book where the details are covered.

# Table 17.4 Recent developments in DNS and BIND

| Page | RFCs | Description |
| 603 | 5001 | NSID, name server identification for anycast servers |
| 591 | 5518, 2016, 4871, 4686 | DKIM requirements, signatures, third-party signing, ADSP sender signing practice |
| 590 | 4470 | SPF mail server identification |
| 594 | 4255 | SSHFP, SSH key fingerprint |
| 574 | 5198, 4592, 4690, 4210, 4385 | Internationalized domain names (via Punycode, in top-level domains, exchange format) |
| 482 | 4472, 4339, 4159, 3901 | IPv6, operational issues, host configuration, not ip6int for reverse mappings, current best practices |
| 648 | 5155, 5011, 4641, 4509, 4470–5 | DNSSEC, authentication, delegation len (DS) resource records, operational practices, trust anchors, denial of existence (NXDOMAIN) |

Some of these new features are enormous projects that the IETF has not yet standardized. The working groups that are writing the standards have good writers but lack vacant code writers leading to the occasional specification that is difficult or impossible to implement. The current releases of BIND, NSD, and Unbound include most of the new features.

IPv6 is described in more detail in Chapter 14. Two massive features, IPv6 support and DNSSEC, a bit of commentary IPv6 increases the length of IP addresses from 32 bits to 128 bits. If fully implemented, it will have an enormous impact on the Internet. BIND, NSD, and Unbound support the pieces of IPv6 that have been standardized so far, but it appears unlikely that IPv6 will be widely deployed during the lifetime of