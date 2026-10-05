# Chapter 17 DNS: The Domain Name System

book. Therefore, our coverage of IPv6 support is brief. There's enough in this chapter to give you the general flavor, but not enough to enable you to migrate your site to IPv6 and configure DNS for it.

The DNSSEC adds authentication data to the DNS database and its servers. It uses public key cryptography to verify the source and integrity of DNS data uses DNS to distribute keys as well as host data.

Sites that deploy DNSSEC-signed zones will run up against a bootstrap problem until the root and top-level domains are signed, because the DNSSEC trust model requires signatures to be chained from the root down. However, a new stopgap called DLV, domain locals validation, is poised to seed in and glue records together until the root and gTLDs are fully onboard with DNSSEC. See page 66 for details.

The introduction of internationalized domain names, which allow the use of nonEnglish characters, is proceeding by way of a hash that maps Unicode characters to ASCII. A system called Punycode performs the mapping uniquely and reversibly by an algorithm known as Bootstrap; RFC3492 for details. Internationalized domain names effectively reduce the maximum length (both per-component and total) allowed for DNS names. The Punycode representation of a name begins with the string--, so if you see strange queries that start with those four characters, you'll know what they represent.

Each of these major issues (IPv6, DNSSEC, and internationalization) significantly increases the size of DNS data records, making it more likely that DNS will bump into limits on UDP packet sizes and require the EDNS0 (Extended DNS, version 0) protocol to increase its packet size from 512 bytes (the default) to a larger value, 4,096 bytes. As of 2009, statistics collected at the K root server show that approximately 35% of queries are not using EDNS0 and would receive truncated or fragmented DNS answers from sites that use larger packets.

# 17.8 THE DNS DATABASE

A zone's DNS database is a set of text files maintained by the system administrator on the zone's master name server. These files are called zone files. They contain two types of entries: parser commands (like things $ORIGIN and $TTL) and resource records. Only the resource records are really part of the database; the parser commands just provide shorthand ways to enter records.

# Commands in zone files

Commands can be embedded in zone files to make them more readable and easier to maintain. The commands influence the way that the parser interprets subsequent records or expand into multiple DNS records themselves.

Zone file commands are standardized in RFCs 1035 and 2308.

+   9. See k.root-servers.org/statistics/GLOBAL/monthly for current data.