# TCP/IP and Network Management
CHAPTER 7

port have been defined in RFC 1700. Some of these well-known ports are listed in Table 7.4.

# Table 7.4 Some Well-Known Port Numbers

| Port/Protocol | Name | Use |
|---|---|--|
| 7/tcp | echo | Echoes everything it receives |
| 13/tcp | daytime | Sends back the current date |
| and time | | |
| 23/tcp | Telnet | Remote terminal emulation |
| 25/tcp | smtp | Email transfer |
| 53/udp | domain | Domain Name System |
| 80/tcp | www | World Wide Web traffic |
| 110/tcp | pop3 | Post Office Protocol, version 3 |
| 443/tcp | https | Secure Web traffic |

# Sockets

In network parlance, a socket is a network connection between two processes, which may be running on the same or different processes. Technically, an open socket has four parts (source host, source port, destination host, and destination port). A closed socket has only the source port and source host.

Note that a socket has ports on both sides of the connection. When a client tries to connect to a server, it first asks the system for a free port (one that isn't being used by any other program). It then asks the system to connect to a destination host and port using that source port. That is why there can be several programs connected between the same hosts; for example, a browser can have two or more windows open to the same host. The system keeps track of both the source and destination port, and has different sockets for each.

# Configuring the Network

In every modern Linux distribution, basic network configuration is done at installation time, when configuring the base system. With all other UNIX systems, all configuration data is stored in text files in the /etc tree.