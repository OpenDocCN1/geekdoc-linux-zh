These two calls are exactly the same as sendto() and recvfrom(), but without the last two parameters, as this information has already been set up by connect(). The send() and recv() calls can also be used for communication on connection based sockets, as here a process's communication partner has already been permanently established.

# 17.5.10 Socket Support Calls

In addition to the main set of system calls associated with socket use, which you have now seen, there are a number of support functions which also need a mention. These are related to hostnames, port numbers, standard network services and network byte ordering.

The gethostname() system call allows processes to have access to the local hostname. The form of the call is:

```
gethostname(name, len)
```

Where name is a pointer to a char array that will hold the host's domain name, and len is the maximum name length that the array can hold. For privileged (EUID=0) processes, sethostname() can be used to set the local hostname to a specified string.

Once you have a host's domain name available you need to be able to get its IP address or vice versa. The library functions gethostbyname() and gethostbyaddr() perform these tasks. The general form of these calls is:

```
hostent = gethostbyname(name)
hostent = gethostbyaddr(addr, len, type)
```

The name parameter is a pointer to a char array containing the host's domain name. The addr parameter is a pointer to a host address of length len and address type type. Both calls return a pointer to a struct hostent, defined in <netdb.h>, which contains name, address and address type information for the required host.

There are a set of well-known ports for all the standard network services, and to find the port associated with a particular service name and protocol there is a standard library function called getservbyname(). This has the general form:

```
servent = getservbyname(name, protocol)
```

The name parameter is a pointer to a string containing the name of the required service and the prototype parameter is a pointer to a string containing the appropriate communication protocol (udp or tcp). This function looks up the required information in the file /etc/services and returns a pointer to a structure of type struct servent filled in appropriately. The servent structure is declared in <netdb.h>.

Different machines with different processor architectures store integer values in several different ways. The most important difference as far as networking is concerned is the order in which the bytes are stored in an integer. Some processors,