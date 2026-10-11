# Internet Services

Before you have fun working with TCP/IP in this chapter, you need to learn about some additional facilities as TCP/IP pertains to Internet services.

# Examining the /etc/services File

Your Linux system has a text file, usually named /etc/services. This file is described in the man page services(5). This file maps the user-friendly names of certain Internet services to a port number and protocol. The precise pathname for this file is given by the C language macro _PATH_SERVICES. A simple example of its use follows:

```
`#include <netdb.h>

printf("File is path '%s\'\n', _PATH_SERVICES);`
```

The preceding code shows the necessary include file netdb.h and a printf(3) statement, which prints out the pathname for the services file.

Each text line in the /etc/services file describes one Internet service. It has the following general format:

service-name port/protocol [alias ...]

The square brackets shown indicate that the one or more alias entries are optional. The /etc/services text line is described in detail in Table 7.1.

# Table 7.1: The /etc/services Fields

| Field | Description |
| --- | --- |
| service-name | The case-sensitive user-friendly name of the service is described by this table entry. |
| port | The port number precedes the slash, and is the decimal port number for the service. |
| / | This separates the port number from the protocol field. |
| protocol | This specifies the type of the protocol to be used. This should be a protocol that can be found in the protocols(5) file. Common examples are udp and tcp. |
| alias | Other names for the "service-name." Additional aliases can be separated by tabs or spaces. There is a maximum of 35 aliases permitted, due to restrictions in getservent(3). |

Following is a pair of well-known service entries:

ftp 21/tcp
telnet 23/tcp

The first entry shown lists the ftp service as being available on TCP/IP port 21. The second entry shows the telnet service being available on TCP/IP port 23.