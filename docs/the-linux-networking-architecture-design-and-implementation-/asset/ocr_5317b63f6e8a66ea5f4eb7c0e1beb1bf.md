# ksruhe.de#0.0.0.0 0.0.0.0 0.0.0.0 0.0.0.0 0.0.0.0 0.0.0.0 0.0.0.0)
EOL

15:37:56.261172 rstud1.rz.uni-ksruhe.de > isdn216-10.rz.uni-ksruhe.de:
icmp: echo reply (ttl 253, id 28562, optlen=40 RR|isdn216-10.rz.uni-
ksruhe.de=rzasc01.rz.uni-ksruhe.de 129.137.96 rzstud1.rz.uni-
ksruhe.de# r-ascend-netz.rz.uni-ksruhe.de rzasc01.rz.uni-ksruhe.de#
0.0.0.0 0.0.0.0 0.0.0.0 (EOL)

**Programming Access** We will show you how IP packet options can be accessed during programming. This example uses Version 1.38. When ping starts, the first thing is to check the parameters passed. If they include -R, then the Echo Request packet has to include the Record Route IP option. For this purpose, ping uses the setsockopt() function to inform an existing socket packet options.

The following example shows how this function is invoked from within the source code of ping:

```
if (setsockopt(s, IPPRTO_IP, IP_OPTIONS, rspace, sizeof(rspace)) < 0)
{
    perror("ping: record route");
    exit(1);
}
```

The specified options will be set in each packet sent over this socket in the future. The IPPRTO_IP parameter means that the packet option to be set is an IP option. This does not necessarily mean that it is an IP option in the true sense. It could be present in another position within the IP header (e.g., IP_TTL also belongs to the IPPRTO_IP group). From the programming perspective, we always have to assume that the current kernel implementation does not support the desired IP option. In this case, setsockopt() returns the value 1 and outputs an error message. Subsequently, an arbitrary number of packets with the packet option set sent over this socket.

Incoming ICMP packets sent by ping are checked for their options as follows: An option pointer points to the First Field in the protocol header is computed. The option pointer is incremented so that it points to the next for. The Record Route option pointer has to point to a byte that includes the number "7". ping doesn't actually have to take care of this value; like all other option-specific constants, it is defined in <linux/ip.h>:

```
#define IPOPT_END (0 |IPOPT_CONTROL)
#define IPOPT_NOOP (1 |IPOPT_CONTROL)
#define IPOPT_SEC (2 |IPOPT_CONTROL|IPOPT_COPY)
#define IPOPT_LSRR (3 |IPOPT_CONTROL|IPOPT_COPY)
#define IPOPT_TIMESTAMP (4 |IPOPT_CONTROL|MEASUREMENT)
#define IPOPT_RR (7 |IPOPT_CONTROL)
#define IPOPT_SID (8 |IPOPT_CONTROL|IPOPT_COPY)
#define IPOPT_SWRR (9 |IPOPT_CONTROL|IPOPT_COPY)
#define IPOPT_RA (20|IPOPT_CONTROL|IPOPT_COPY)
```

If one of these packet options is found, then it is output.