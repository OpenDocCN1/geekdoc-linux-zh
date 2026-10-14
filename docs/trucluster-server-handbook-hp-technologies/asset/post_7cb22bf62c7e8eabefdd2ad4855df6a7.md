
# 16.10.4 The Cluster as a Client

What happens with respect to these dynamically allocated ports when the cluster member is the client? The dynamic port numbers must be unique to the cluster in order to distinguish an application in a particular cluster member from the same application running in another cluster member, and we know that the cluster can have 8 members maximum (at the present time). How many of these dynamic ports are available for use in typical client/server network activities?

The number of available dynamic ports can be discerned by calculating the difference between two inet subsystem attributes - ipport_userreserved (default is 5000) and ipport_userreservedmin (default is 1024). The difference is 3976. Using the default values, this number indicates how many concurrent client activities can be executing within the cluster at any one time. While the 3976 number may be plenty for a single node machine, it is potentially a bottleneck for a multi-member cluster.

HP recommends that the ipport_userreserved attribute be increased to its maximum (65535) on clusters with more than two members. This will provide approximately 63k ports for concurrent use spread across the cluster members. See section 19.3.7.3 for an example modifying ipport_userreserved.

# 16.10.5 The inetd.conf File

The server side of network applications such as telnet and ftp (telnetd or ftpd) is not started until the client has requested access (through the telnet or ftp commands). The server daemons are started up (upon client request) by the inetd daemon, which is responsible for handling the startup of any services listed in the /etc/inetd.conf file. Below is a sample of an inetd.conf file.

```
# cat /etc/inetd.conf
#
#
# Internet server configuration database
#
# Description: The inetd.conf file is the first file that the inetd daemon reads for information on how to handle Internet service requests. It contains global services that can be run on all members in a cluster.
#
# Precedence: Entries in inetd.conf.local will override entries in inetd.conf because it is read after inetd.conf.
#
# Syntax: ServiceName SocketType ProtocolName Wait/NoWait UserName \
ServerPath ServerArgs
# ServiceName name of an Internet service defined in the /etc/services file
# SocketType type of socket used by the service, either stream or dgram
# ProtocolName name of an Internet protocol defined in the /etc/protocols file
```

```
```text
# hostname
clumach4
```
```

```
```text
# ping clu_ftp_den
PING clu_ftp_den (192.168.0.171): 56 data bytes

---clu_ftp_den PING Statistics---
3 packets transmitted, 0 packets received, 100% packet loss
```
```

```
```text
# grep den /etc/hosts
192.168.0.171    clu_ftp_den
```
```

The cluster member also has the alias name and IP address reflected in the /etc/hosts file:

```
```text
[molari]
# grep den /etc/hosts
192.168.0.171    clu_ftp_den
```
```

Create the alias on cluster member molari.

```
```text
[molari]
# /usr/sbin/cluamgr -a aliasclu_ftp_den
```
```

```
```text
[molari]
# /usr/sbin/cluamgr -s clu_ftp_den

Status of Cluster Alias: clu_ftp_den

netmask: 0
aliasid: 2
flags: <ENABLED,IP_V4>
connections recvd from net: 0
connections forwarded: 0
connections recvd within cluster: 0
data packets received from network: 0
data packets forwarded within cluster: 0
datagrams received from network: 0
datagrams forwarded within cluster: 0
datagrams received within cluster: 0
fragments received from network: 0
fragments forwarded within cluster: 0
fragments received within cluster: 0
Member Attributes:
memberid: 2, selw=1, selp=1, ipr1=flags=10<ENABLED>
```
```

The alias has not been joined, and aliasd is not yet aware of the new alias. Let’s correct that situation.

```
```sh
[molari]
# /usr/sbin/cluamgr -a alias=clu_ftp_den,join
```
```

```
```text
[molari]
# /usr/sbin/cluamgr -s clu_ftp_den

Status of Cluster Alias: clu_ftp_den

netmask: 0
aliasid: 2
flags: 5 ENABLED, IP_V4>
connections recv from net: 0
connections forwarded: 0
connections rcvd within cluster: 0
data packets received from network: 0
data packets forwarded within cluster: 0
datagrams received from network: 0
datagrams forwarded within cluster: 0
datagrams received within cluster: 0
fragments received from network: 0
fragments forwarded within cluster: 0
fragments received within cluster: 0
Member Attributes:
memberid: 2, selw=1, selp=1, prio=1 flags=11<JOINED,ENABLED>
```
```

```
```sh
[molari]
# /usr/sbin/cluamgr -r start
```
```

From the client system:

```
```text
# ping clu_ftp_den

PING clu_ftp_den (192.168.0.171): 56 data bytes
64 bytes from 192.168.0.171: icmp_seq=0 ttl=64 time=1 ms
64 bytes from 192.168.0.171: icmp_seq=1 ttl=64 time=0 ms

---clu_ftp_den PING Statistics---
2 packets transmitted, 2 packets received, 0% packet loss
round-trip (ms) min/avg/max = 0/0/1 ms
```
```

```
```text
# telnet clu_ftp_den

Trying 192.168.0.171...
Connected to clu_ftp_den.
Escape character is '^]'.

Compaq Tru64 UNIX V5.1A (Rev. 1885) (molari.dec.com) (tpts/1)

login: root

# exit

Connection closed by foreign host.
```
