Typically, client processes and unknown/private servers use dynamic ports. These ports are also used to test server processes.

# EXERCISE 20.6

Browse the IANA website. What is the total number of services that have been assigned port numbers?

# EXERCISE 20.7

Browse through the /usr/include/sys/socket.h file. How many communication domains and service types have been defined?

# 20.6.6 Important Data Structures and Related Function Calls

UNIX provides many functions to network programmers to manipulate IP addresses. Most of these functions use data structures for storing socket names, that is, IP addresses, port numbers, address sizes, and other related information. A few are used to maintain information about a host on the Internet and an Internet service.

# 20.6.6.1 Important Data Structures for IP Addresses, Hosts, and Services

A brief summary of the most important data structures for network-based IPC and network programming is given in Table 20.3. These data structures deal with socket addresses, information about hosts on the Internet, and information about Internet services. Discuss the use of these data structures and their internal details in this section. The system calls, library calls, and macros that deal with them are discussed in the sections that follow.

```
struct sockaddr {
	unsigned short sa_family;
	char sa_data[14];
};
```

The sa_family field contains the socket address family and the sa_data contains the actual socket address. The value of sa_data is interpreted based on the value of sa_family. The address family used for UNIX domain sockets is AF_LOCAL (or AF_UNIX). For Internet domain sockets, it is AF_INET or AF_INET6. When sa_family is AF_LOCAL, the sa_data field is supposed to contain a pathname as the socket's address. When sa_family is AF_INET, the sa_data field contains