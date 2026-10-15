The line `domain example.domain` instructs the resolver to append `example.domain` to every hostname without a domain part. This means a query for `mailserver` will be sent to the DNS server as a query for `mailserver.example.domain`. The line beginning with `search` has no effect on this system; it is used to determine the domain or subdomain to be searched first. Assume that the domain `example.domain` belongs to a company with branches in the U.S., Germany, France, Italy, and the U.K. It would make sense to create subdomains for the different countries, thus resulting in subdomains named `boston.example.domain`, `munich.example.domain`, and so forth. The search entry for a system in the U.S. would look similar to the one shown in Listing 5.18.

**LISTING 5.18** `resolv.conf` for Subdomains

```text
nameserver 192.168.0.200 192.168.1.200 192.168.1.201
domain boston.example.domain
search boston.example.domain example.domain
```

The search for a hostname without a domain part would use the server with the IP address `192.168.0.200` asking for `hostname.boston.example.domain` first. If the system cannot be found, the query would use `hostname.example.domain`. If this query should also fail, the next DNS server in the list (`192.168.1.200`) would be used and so forth. If the list of possible DNS servers is exhausted and no answer is found, the query would return an error. A system like the one mentioned works best if most of the queries stay in the respective network. Queries regarding systems in other subdomains have to be relayed to the respective subdomain in the system belongs to, thus requiring the local name server to “know” about the name servers responsible for the other subdomains. The files `hosts`, `nsswitch.conf`, and `resolv.conf` have to be consistent for all systems capable of processing the queries within a subdomain.

One file that has to be consistent for security reasons is `sshd_config`. The file configures the behavior of the ssh daemon, which means the configuration of the allowed encryption algorithms to establish a connection and the protocol to be used, among other things. If all clients use a current release of the software, then the `Protocol` entry should contain only 2 (see Section 7.4.1, “Why Use ssh?”).

The `passwd` file does not seem to fit the other files mentioned so far, but only at first sight. If the UIDs and GIDs for the users and the groups used on more than one system are consistent on all systems, then moving a user from one system to another is much easier. Besides that, it is possible to use the UID to include an employee number or other information, provided the UID is large enough. Listing 5.19 shows an example.