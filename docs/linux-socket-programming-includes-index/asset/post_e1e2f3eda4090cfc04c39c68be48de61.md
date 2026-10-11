
## HTTP 1.1 Status Codes

If you want to write your own Web server, you need to understand and use the standard status codes of HTTP 1.1 (RFC2616, RFC2817). Table A.3 lists these codes.

**TABLE A.3** HTTP Result Codes

| Code Class Value | Class Name | Specific Code and Description |
| :--- | :--- | :--- |
| 1xx | Informational | 100 Continue |
| | | 101 Switching Protocols |
| 2xx | Successful | 200 OK |
| | | 201 Created |
| | | 202 Accepted |
| | | 203 Non-Authoritative Information |
| | | 204 No Content |
| | | 205 Reset Content |
| | | 206 Partial Content |
| 3xx | Redirection | 300 Multiple Choices |
| | | 301 Moved Permanently |
| | | 302 Moved Temporarily |
| | | 303 See Other |
| | | 304 Not Modified |
| | | 305 Use Proxy |
| 4xx | Client Error | 400 Bad Request |
| | | 401 Unauthorized |
| | | 402 Payment Required |
| | | 403 Forbidden |
| | | 404 Not Found |
| | | 405 Method Not Allowed |
| | | 406 Not Acceptable |
| | | 407 Proxy Authentication Required |
| | | 408 Request Timeout |
| | | 409 Conflict |
| | | 410 Gone |
| | | 411 Length Required |
| | | 412 Precondition Failed |
| | | 413 Request Entity Too Large |
| | | 414 Request-URI Too Long |
| | | 415 Unsupported Media Type |
| 5xx | Server Error | 500 Internal Server Error |
| | | 501 Not Implemented |
| | | 502 Bad Gateway |
| | | 503 Service Unavailable |
| | | 504 Gateway Timeout |
| | | 505 HTTP Version Not Supported |

### Socket Options (get/setsockopt())

Tables A.4 through A.7 list the various socket options and the required parameters. Not all options are size compatible between UNIX types. For example, IP_TTL in Linux allows a type int, but only fills the first byte. IBM's AIX restricts the same option to a char instead.

| Level | Option | Description | * | R | W | Value | Type |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| SOL_SOCKET | SO_ATTACH_FILTER | Attach filter | ? | ? | ? | Integer | int |
| SOL_SOCKET | SO_BINDTODEVICE | Bind to device | ? | ? | ? | String | char* |
| SOL_SOCKET | SO_BROADCAST | Enable broadcast | Y | Y | Y | Boolean | int |
| SOL_SOCKET | SO_BSDCOMPAT | Request BSD bug-for-bug compatibility | Y | Y | Y | Boolean | int |
| SOL_SOCKET | SO_DEBUG | Enable socket debugging | Y | Y | Y | Boolean | int |
| SOL_SOCKET | SO_DETACH_FILTER | Detach filter | ? | ? | ? | Integer | int |
| SOL_SOCKET | SO_DONTROUTE | Forbid routing | Y | Y | Y | Boolean | int |
| SOL_SOCKET | SO_ERROR | Last error | Y | Y | Y | Integer | int |

**TABLE A.4 Continued**

| Level | Option | Description | R | W | Value | Type |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| SOL_SOCKET | SO_KEEPALIVE | Enable keeping connection alive | Y | Y | Y | Boolean | int |
| SOL_SOCKET | SO_LINGER | Linger until data sent | Y | Y | Y | Linger | struct linger |
| SOL_SOCKET | SO_NO_CHECK | No checking | Y | Y | Y | Boolean | int |
| SOL_SOCKET | SO_OOBINLINE | Place out-of-band inline | Y | Y | Y | Boolean | int |
| SOL_SOCKET | SO_PASSCRED | Enable passing user credentials | Y | Y | Y | Boolean | int |
| SOL_SOCKET | SO_PEERCREDS | Peer Credentials | Y | Y | Y | Credentials | struct ucred |
| SOL_SOCKET | SO_PRIORITY | Set the queue priority | Y | Y | Y | Integer | int |
| SOL_SOCKET | SO_RCVBUF | Receive buffer size | Y | Y | Y | Integer | int |
| SOL_SOCKET | SO_RCVLOWAT | Receive low water mark | Y | Y | N | Integer | int |
| SOL_SOCKET | SO_RCVTIMEO | Receive Timeout | Y | Y | Y | Time | struct timeval |
| SOL_SOCKET | SO_REUSEADDR | Reuse Address | Y | Y | Y | Boolean | int |
| SOL_SOCKET | SO_REUSEPORT | Reuse Address (multicasting) | N | - | - | Boolean | int |
| SOL_SOCKET | SO_SECURITY_AUTHENTICATION | Security authentication | N | - | - | Integer | int |
| SOL_SOCKET | SO_SECURITY_ENCRYPTION_NETWORK | Security encryption network | N | - | - | Integer | int |
| SOL_SOCKET | SO_SECURITY_ENCRYPTION_TRANSPORT | Security encryption transport | N | - | - | Integer | int |
| SOL_SOCKET | SO_SNDBUF | Send buffer size | Y | Y | Y | Integer | int |
| SOL_SOCKET | SO_SNDLOWAT | Send low water mark | Y | Y | Y | Integer | int |
| SOL_SOCKET | SO_SNDTIMEO | Send Timeout | Y | Y | Y | Time | struct timeval |
| SOL_SOCKET | SO_TYPE | Socket Type | Y | Y | Y | Integer | int |

**TABLE A.5 IP-Level Socket Options**

| Level | Option | Description | * | R | W | Value | Type |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| SOL_IP | IP_ADD_MEMBERSHIP | Add multicast membership | Y | Y | Y | IPv4 Multicast Address | struct in_addr |
| SOL_IP | IP_DROP_MEMBERSHIP | Drop multicast membership | Y | Y | Y | IPv4 Multicast Address | struct in_addr |
| SOL_IP | IP_HDRINCL | Enable manual IP header creation | Y | Y | Y | Boolean | int |
| SOL_IP | IP_MTU_DISCOVER | MTU discover | Y | Y | Y | Integer | int |
| SOL_IP | IP_MULTICAST_IF | Outgoing multicast interface | Y | Y | Y | IPv4 Address | struct in_addr |
| SOL_IP | IP_MULTICAST_LOOP | Enable multicast loopback | Y | Y | Y | Boolean | int |
| SOL_IP | IP_MULTICAST_TTL | IP Multicast TTL | Y | Y | Y | Integer | int |
| SOL_IP | IP_OPTIONS | IP options | Y | Y | Y | Options | int [] |
| SOL_IP | IP_PKTOINFO | Enable getting packet info | Y | Y | Y | Boolean | int |
| SOL_IP | IP_RECPOPTNS | Packet options | N | - | Y | Options | int [] |
| SOL_IP | IP_RECVERR | Enable receive error packets | Y | Y | Y | Boolean | int |
| SOL_IP | IP_RECVOPTS | Enable receive options | Y | Y | Y | Boolean | int |
| SOL_IP | IP_RECVTOS | Get received TOS | Y | Y | Y | Integer | int |
| SOL_IP | IP_RECVTTL | Get received TTL | Y | Y | Y | Integer | int |
| SOL_IP | IP_MULTICAST_IF | Multicast interface | * | Y | Y | Integer | int |
| SOL_IP | IP_MULTICAST_TTL | Multicast TTL | * | Y | Y | Boolean | int |
| SOL_IP | IP_MULTICAST_LOOP | Multicast loop | * | Y | Y | Boolean | int |
| SOL_IP | IP_TOS | Type of Service (TOS) | * | Y | Y | Integer | int |
| SOL_IP | IP_TTL | Time to Live (TTL) | * | Y | Y | Integer | int |

**TABLE A.6 IPv6-Level Socket Options**

| Level | Option | Description | * | R | W | Value | Type |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| SOL_IPV6 | IPV6_ADD_MEMBERSHIP | Join multicast membership | ? | ? | ? | IPv6 Multicast Address | struct ip_mreq6 |
| SOL_IPV6 | IPV6_ADDRFORM | Change address for socket | ? | ? | ? | Integer | int |
| SOL_IPV6 | IPV6_AUTHHDR | Offset of AUTHHDR | ? | ? | ? | Integer | int |
| SOL_IPV6 | IPV6_CHECKSUM | Offset of raw checksum for raw sockets | ? | ? | ? | Integer | int |
| SOL_IPV6 | IPV6_DROP_MEMBERSHIP | Drop multicast membership | ? | ? | ? | IPv6 Multicast Address | struct ip_mreq6 |
| SOL_IPV6 | IPV6_DSTOPTS | Enable getting destination options | ? | ? | ? | Boolean | int |
| SOL_IPV6 | IPV6_HOPLIMIT | Enable getting hop limit | ? | ? | ? | Boolean | int |
| SOL_IPV6 | IPV6_HOPOPTS | Enable getting hop-by-hop options | ? | ? | ? | Boolean | int |
| SOL_IPV6 | IPV6_MULTICAST_HOPS | Specify number of multicast hops | ? | ? | ? | Integer | int |
| SOL_IPV6 | IPV6_MULTICAST_IF | Specify outgoing multicast interface | ? | ? | ? | IPv6 Address | struct in6_addr |
| SOL_IPV6 | IPV6_MULTICAST_LOOP | Enable multicast loopback | ? | ? | ? | Integer | int |
| SOL_IPV6 | IPV6_NEXTHOP | Enable specifying next hop | ? | ? | ? | Boolean | int |
| SOL_IPV6 | IPV6_PKTINFO | Receive packet information | ? | ? | ? | Integer | int |
| SOL_IPV6 | IPV6_RCVTCLASS | Specify packet tclass | ? | ? | ? | Options | int [] |
| SOL_IPV6 | IPV6_ROUTER_ALERT | Enable router alerts | ? | ? | ? | Boolean | int |
| SOL_IPV6 | IPV6_RSRCRT | Receive source route | ? | ? | ? | Boolean | int |
| SOL_IPV6 | IPV6_UNICAST_HOPS | Specify hop limit | ? | ? | ? | Integer | int |
