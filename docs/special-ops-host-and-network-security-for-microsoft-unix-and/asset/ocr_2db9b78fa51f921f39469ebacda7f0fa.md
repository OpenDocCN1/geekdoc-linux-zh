# Tools & Traps...

# Using the Bogons List

A maintained listing of IP addresses that are not currently in use or should never be seen on the public Internet is available at www.cymru.com/Documents/bogon-list.html. This list is known as the Bogons List. Since the creation of the Bogons List by Rob Thomas, it has become good practice to block these IP addresses at network borders and within applications because they can be used for illegitimate traffic.

Remember to keep up to date with this list because new IP blocks are changed or reassigned regularly.

# Exploiting DNS

Depending on the skill level of an attacker, exploiting DNS can be trivial (see Table 8.7). Advanced vulnerabilities such as cache poisoning, DoS, and buffer overflows can manipulate server response, or even compromise an entire system. Simplistic vulnerabilities, zone transfers, and version lookups, however, are only information disclosure risks and usually do not breach DNS security.

# Table 8.7 Common DNS Attacks

| Name | Vulnerabilities | Vulnerability Rating | Attack Method |
|---|---|---|---|
| Zone transfer | Information disclosure of hosted domain names | Low | Performing an unrestricted zone transfer, or for forge appropriate approval. |
| Version lookups | Disclosure of software version | Low | Performing lookup of version file to aid future exploitation. |
| DoS | Overworking a system's limited resources, leading to system or service inaccessibility | Medium | Sending or requesting more resources than available. |