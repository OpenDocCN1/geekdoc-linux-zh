
host on the Internet. IPv4 addresses are 32 bits long and IPv6 addresses are 128 bits long. On a host with a given IP address and running multiple servers, a port number allows the operating system kernel of the host to direct an incoming client request to a particular server on the host. Thus, the <IP address, port number> pair uniquely identifies the location of a service on the Internet, offered using different transport-layer protocols such as TCP and UDP.

A port number is a positive integer in the range 0 to 65535. The purpose of a port number is to distinguish different services offered on a host. The International Assigned Numbers Authority (IANA) assigns port numbers and service names. Service names are assigned on a first-come, first-served basis and port numbers are assigned according to a particular scheme, described in RFC6335 (see Table 20.26). Table 20.12 describes the general scheme used by IANA for the allocation of ports.

According to RFC6335, system ports and user ports are assigned by IANA using different processes. Dynamic ports are never assigned and may be used by any process randomly. System ports are used to offer well-known services and are, therefore, also known as well-known ports. Normally, the well-known ports are offered at the same port number regardless of the transport-level protocol used by the service (TCP, UDP, etc.). Note that only a superuser (i.e., root) can use ports < 1024. A few well-known services and their respective port numbers are listed in Table 20.13.

## TABLE 20.12 Port Numbers and their Purpose

| Port Number Range | Purpose |
|---|---|
| 0–1023 | System/well-known Ports |
| 1024–49151 | User/registered Ports |
| 49152–65535 | Dynamic/private Ports |

## TABLE 20.13 Some Well-Known Services and their Ports

| Well-Known Service | Port |
|---|---|
| ECHO | 7 |
| DAYTIME | 13 |
| QOTD (Quote-of-the-Day) | 17 |
| FTP-DATA | 20 |
| FTP (File Transfer Protocol) | 21 |
| SSH (Secure Shell) | 22 |
| TELNET | 23 |
| SMTP (Simple Mail Transfer Protocol) | 25 |
| TIME | 37 |
| FINGER | 79 |
| HTTP, WWW | 80 |
| KERBEROS | 88 |
| POP3 | 110 |
| SFTP | 115 |

Typically, client processes and unknown/private servers use dynamic ports. These ports are also used to test server processes.

## EXERCISE 20.6

Browse the IANA website. What is the total number of services that have been assigned port numbers?

## EXERCISE 20.7

Browse through the /usr/include/sys/socket.h file. How many communication domains and service types have been defined?

## 20.6.6 Important Data Structures and Related Function Calls

UNIX provides many functions to network programmers to manipulate IP addresses. Most of these functions use data structures for storing socket names, that is, IP addresses, port numbers, address sizes, and other related information. A few are used to maintain information about a host on the Internet and an Internet service.

### 20.6.6.1 Important Data Structures for IP Addresses, Hosts, and Services

A brief summary of the most important data structures for network-based IPC and network programming is given in Table 20.3. These data structures deal with socket addresses, information about hosts on the Internet, and information about Internet services. Discuss the use of these data structures and their internal details in this section. The system calls, library calls, and macros that deal with them are discussed in the sections that follow.

```
struct sockaddr {
	unsigned short sa_family;
	char sa_data[14];
};
```

The sa_family field contains the socket address family and the sa_data contains the actual socket address. The value of sa_data is interpreted based on the value of sa_family. The address family used for UNIX domain sockets is AF_LOCAL (or AF_UNIX). For Internet domain sockets, it is AF_INET or AF_INET6. When sa_family is AF_LOCAL, the sa_data field is supposed to contain a pathname as the socket's address. When sa_family is AF_INET, the sa_data field contains both an IP address and a port number. The sockaddr_in structure is specifically used for this purpose.

### struct sockaddr_un

The address structure for the address of a UNIX domain socket is defined in sys/un.h as

```
struct sockaddr_un {
    uint8_t      sun_len;
    sa_family_t  sun_family;
    char         sun_path[104];
};
```

Here, sun_len is the length of sockaddr_un including the NULL byte, sun_family is AF_LOCAL (or AF_UNIX), and sun_path[104] is the null-terminated pathname in the file system structure that refers to the socket.

### struct sockaddr_in

This structure may be used to hold the address information for an Internet domain socket. It is defined in the /usr/include/sys/socket.h file as follows:

```
struct sockaddr_in {
    uint8_t      sin_len;
    sa_family_t  sin_family;      /* short int */
    in_port_t    sin_port;        /* unsigned short */
    struct in_addr sin_addr;
    unsigned char sin_zero[8];
};
```

The sin_family field specifies the address family; usually this is AF_INET. The sin_port and sin_addr fields contain a 16-bit port number and a 32-bit IPv4 address in network byte order, respectively. The sin_zero field is set to NULL (i.e., '0') as it is not used. The in_addr structure is defined as follows.

```
struct in_addr {
    unsigned long s_addr;
};
```

### struct hostent

The hostent structure may be used to hold official information about a host on the Internet. It is defined in the /usr/include/netdb.h file as follows:
