# The Hacking Top 10 • Chapter 5

a tool to be used as a “hack tool” it only needs to be in the hands of someone both knows how to use it, and has something devious in mind. They do not have to dump users, steal information, or pop admin. Be so advised, anything with a legitimate administrative purpose can be used to do something in a way in which the developer’s never intended.

So, without further ado, here is the top 10:

+   1. netcat
2. nmap
3. nessus
4. nikto
5. wireshark
6. Canvas/Core Impact
7. metasploit
8. paros
9. hping2
10. ettercap

# Netcat

Commonly referred to as, the “Transmission Control Protocol (TCP)/Internet Protocol (IP) Swiss Army Knife,” netcat is a simple UNIX-based utility (although it does have a Windows command-line version) that sends data across a network using either TCP or User Datagram Protocol (UDP). While not a hacker utility per se, it is so prolific that it needed to be included. It can be used from the command line by itself, or integrated as part of a script. It is so simple and lightweight, yet so flexible and powerful, that it has become a favorite of both hackers and security professionals worldwide. According to www.vulynch.org/netcat/, the current version is Netcat 1.1, released on March 20, 1996. It includes the ability to perform tunneling with the ability to control all data packet parameters to include source port/interface, listening port/interface, and destination port/interface. Additionally, it has built in port scanning capabilities with randomizer, buffered send mode (i.e., # of packets every # seconds), and original RFC 854² Telnet codes parser and responder.

> www.faqs.org/rfc/rfc854.html