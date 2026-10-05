# Chapter 17 DNS: The Domain Name System

colorado.edu, edu, or the root domain. A referral must include addresses for the servers of the referred-domain, so the choice is not arbitrary; the server must refer to a domain for which it already knows the servers.

The longest answer (the one with the most components) is returned. If the address of lair was not known but the name servers for cs.colorado.edu were known, then those servers' addresses would be returned. If cs.colorado.edu was unknown then the addresses of name servers for colorado.edu would be returned, and so on.

Name servers preload their caches from a "hints" file that lists the servers for the root domain. Some referral can always be made, even if it's just "Ask a root server".

# 17.5 THE DNS NAMESPACE

The DNS namespace is organized into a tree with top-level branches: forward mappings and reverse mappings. Forward mappings map hostnames to IP addresses, and reverse mappings map IP addresses to hostnames. Every fully qualified hostname (e.g., nubark.astrust.com) is a node in the forward branch of the tree, and every IP address is a node in the reverse branch. Period separates levels of the tree; the root (of the top) is "." aka "dot".

Fully qualified hostnames can be viewed as a notation in which the "significant part" is on the right. For example, in the name nubark.astrust.com, nubark is in at and trust is in com. IP addresses, on the other hand, have the "most significant part" on the left. In 128.18.243.100, for example, host 100 is on subnet 243, which is part of network 128.138.

To allow the DNS system to service both kinds of data, the IP branch of the namespace is inverted by litting the octets of the IP addresses. For example, if nubark.astrust.com has IP 63.173.189.1, the corresponding node of the forward branch of the naming tree is "nubark.astrust.com." and the node of the reverse is "1.189.173.63.in-addr.arpa." Both of these names end with a dot, just as the pathnames of files always start with a slash.

A "fully qualified domain name" is the full path to a DNS object, including a final dot. For example, a host nubark in astrust domain contains the FQDN "nubark.astrust.com."

A "domain" is a subtree of the DNS naming tree. For example, the astrust domain contains astrust.com and all of astrust.com's subdomains and hosts. By contrast, a "zone" is any domain subdomains that have been delegated to other names.

If the astrust domain were further subdivided into the subdomains engineering, marketing, and booklab, then the astrust domain would contain four zones: the original astrust.com plus engineering.astrust.com, marketing.astrust,

+   1. The in-addr.arpa portion of the name is a fixed suffix.