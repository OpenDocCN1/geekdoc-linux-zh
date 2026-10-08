# CHAPTER 9 | Networked Application Security

When a client computer searches for the IP address associated with a domain name, it first looks in the database associated with the local DNS server. If that domain name is not found locally, DNS server may be configured to send the request to another DNS server. If the domain name is still not found, that request may be sent to one of the root nameservers. That search process is known as a recursive query.

A substantial number of DNS servers may be involved in a search for a domain name. That provides plenty of opportunity for a black-hat hacker to jump into the search to redirect unsuspecting users to fake domains. To that end, DNS is a frequent target of attacks. One way to redirect unsuspecting users to fake domains is based on an attack known as cache poisoning.

# DNS Network Configuration

With such potential vulnerabilities in mind, you may consider configuring different kinds of DNS servers on different parts of a network. To that end, it's important to protect the master authoritative DNS server for your network. Review the network configuration shown in Figure 9-2. It is the same configuration shown in Chapters 6 and 7, with DNS servers added.

![](bbox=[0.065, 0.435, 0.935, 0.955])