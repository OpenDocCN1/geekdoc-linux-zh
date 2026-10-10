
## 19. What will be the effect of a computer having the following two lines in `/etc/ntp.conf`?

```
server pool.ntp.org
server tardis.example.org
```

- **A.** The local computer's NTP server will poll a server in the public NTP server pool; the first `server` option overrides subsequent `server` options.
- **B.** The local computer's NTP server will poll the `tardis.example.org` time server; the last `server` option overrides earlier server options.
- **C.** The local computer's NTP server will poll both a server in the public NTP server pool and `tardis.example.org` and use whichever site provides the cleanest time data.
- **D.** The local computer's NTP server will refuse to run because of a malformed `server` specification in `/etc/ntp.conf`.

## 20. You've configured one computer on your five-computer network, `gateway.pangaea.edu`, as an NTP server that obtains its time signal from `ntp.example.com`. This configuration provides an acceptably accurate clock on `gateway.pangaea.edu`. What computer(s) should your network's other computers use as their time source(s)?

- **A.** You should consult a public NTP server list to locate the best server for you.
- **B.** Both `gateway.pangaea.edu` and `ntp.example.com`.
- **C.** Only `ntp.example.com`.
- **D.** Only `gateway.pangaea.edu`.

# Answers to Review Questions

- D. Kerberos is a network authentication tool; clients and servers that are written to use Kerberos can consult with the Kerberos server to perform authentication tasks. DNS is the Domain Name System; it translates between IP addresses and hostnames. DHCP is the Dynamic Host Configuration Protocol; it delivers IP addresses to clients for basic network setup. NTP is the Network Time Protocol; it keeps computers' clocks synchronized. None of these three protocols is used for network authentication, so options A, B, and C are all incorrect.

- D. The `mailq` utility can display a backlog of old messages and show you whether the mail service is functioning. Postfix and sendmail are both mail server programs (although typing `sendmail -bp` is equivalent to typing `mailq`, while `traceroute` is an enhanced version of `ping` that shows the route data takes to reach a target.

- B, D. The Post Office Protocol version 3 (POP3) and the Internet Message Access Protocol (IMAP) are two common protocols used for retrieving e-mail from the final mail servers in the mail delivery chain. The Simple Mail Transfer Protocol (SMTP) is used for sending e-mail, both by the originating system and by mail servers between the originator and the final recipient, but it's not used by e-mail clients to retrieve e-mail from the server. A mail transfer agent (MTA) is another name for an e-mail server program; it's not an e-mail protocol per se.

- A. The `newaliases` command processes the text-mode `/etc/aliases` file into a binary form that the mail server can process more rapidly. This command must be run for your changes to take effect. Options B and C are both fictitious options to real commands, and option C is a fictitious command.

- A. Postfix's configuration file format is easier for nonexperts to understand and manipulate than is sendmail's configuration file format, which is notoriously opaque. Both Postfix and sendmail support SMTP, and neither supports POP or IMAP (although you can run separate POP or IMAP servers alongside either Postfix or sendmail). Neither Postfix nor send-mail directly supports GPG, but you can send GPG-encrypted messages using either mail server by using a mail client or other software to encrypt the message.

- C. The Internet Message Access Protocol (IMAP) enables users to permanently store and organize e-mail on the server, as specified by the question. The Simple Mail Transfer Protocol (SMTP) is a push mail protocol that's not used for mail retrieval by end users. The Post Office Protocol version 3 (POP3) is a pull mail protocol, but it doesn't provide options for organizing mail on the server, so it won't work well for the stated purpose. KMail is one of many mail clients for Linux; it's not a mail protocol at all, although it supports SMTP, POP3, and IMAP.

- A. Sendmail and Postfix both understand the same Simple Mail Transfer Protocol (SMTP) and can therefore send and receive e-mail from each other with no problems, assuming proper configuration; thus, option A is correct. Contrary to options B, C, and D, there are no fundamental incompatibilities that will block e-mail delivery, delay e-mail delivery, or require an intermediate system. (That said, network problems, system load issues, and so on, can unpredictably delay e-mail delivery in the real world, but such delays aren't the result of sendmail/Postfix incompatibilities.)

8. C. The `rndc` program provides a control interface for the DNS server program, *named*. The *flush* option to *rndc* clears (flushes) the cache of recent DNS lookups, so option C is correct. None of the remaining options describes anything that *rndc* can do, although the *reload* option will cause *named* to reload its zone files, which is partway to option A.

9. B. Zone file definitions in */etc/named.conf* tell the DNS server where to look to find mappings of IP addresses to hostnames, or vice versa. The `in-addr.arpa` pseudo-domain is reserved for reverse DNS lookups—the server returns hostnames when given IP addresses. The `file` directive points the server to the file that holds the mappings. Thus, option B is correct. Option A is incorrect because reverse DNS lookups return hostnames, not IP addresses. A zone directive is not an instruction to ignore a domain or address block, contrary to option C. The `type master` line in the example tells the server that it is the master DNS server for this zone, not to retrieve a file from another master server, so option D is incorrect.

10. D. The */var/named* directory holds DNS zone files on a typical Linux DNS server that runs *named*. Options A, B, and C are all fictitious; these locations don’t normally exist.

11. A, B. A DNS server can deliver IP addresses for local users, *off-site* users, or both, depending on its and your network’s configuration; thus, options A and B are both correct. NetBIOS and IPX are alternative network stacks, neither of which uses the TCP/IP addresses that DNS delivers. Thus, options C and D are both incorrect.

12. A, D. Mail exchanger (MX) and canonical name (CNAME) records are common in forward zone files. There are no such things as DNS and ZF records. Other common record types include Address (A), Name Server (NS), Pointer (PTR), and Start of Authority (SOA) records. (PTR records are used in reverse zone files.)

13. C. Option C is correct; an administrative contact e-mail address is embedded in the SOA record, but with the *at-sign* (@) replaced by a dot (.). Option A is incorrect because the serial number need not be date-based, although date-based serial numbers are common.

Option B is incorrect because the primary DNS server for a domain need not be part of the domain it serves. Option D is incorrect because the SOA record identifies only one DNS server; others may be specified via separate NS records.

14. A. The question is asking for an address (A) record entry for the forward zone file, and option A presents such an entry. Option B presents a valid mail exchanger (MX) record, but that’s not what the question asked for. Option C presents a text (TXT) record that might appear in a reverse zone file, but it’s a somewhat odd one. Option D presents a correct pointer (PTR) record for the reverse zone file, but that’s not what the question asked for.

15. B. A canonical name (CNAME) record creates a sort of alias, enabling a second name to access a computer that already has a hostname. Option C correctly describes the effect of the CNAME record in this example, given the address (A) record that also appears in this example. The CNAME entry shown does *not* create a name of *www.tycho.luna.edu*, contrary to option A. E-mail delivery to a domain can be adjusted via an MX record, but the example includes no such record; and even if the second record were an MX record rather than a CNAME record, option C would not describe its effect. The dot at the end of *tycho.luna.edu* in the first entry identifies a complete hostname; it’s either required, or the domain name portion of the name must be omitted (as in *www* on the second line), contrary to option D.
