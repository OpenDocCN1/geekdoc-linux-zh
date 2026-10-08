```
.default:hn=255.255.255.0:dn=example.org:
:ds=192.168.3.150
```

```
# Reference entries for each subnet
.subnetsm=255.255.255.0:gw=192.168.31.1:tc=default:
.doseemu sm=255.255.255.0:gw=192.168.31.1:tc=default:
```

```
# TCP/IP in the DOSEMulator
dosemu-1-tc=.dosemu:ha=64620190787:ip=192.168.31.101
dosemu-2-tc=.dosemu:ha=64620290787:ip=192.168.31.102
dosemu-3-tc=.dosemu:ha=64620390788:ip=192.168.31.103:
```

```
# Real (DOS) computers
pea.example.org:tc=.subnet31:ht=ieee802:
:ha=1005AD262788:ip=192.168.3.155
```

# Listing 22.3 Extract from the file /etc/bootp

An entry (also known as stanza) consists of a name and the associated values. The keyword tc (table continuation) can be used to refer to a template. These references can be multiple, the definition of a reference may turn contain a reference. Listing 22.3 first defines a default entry (.default) which contains the domain (dn), the name server (ds), and the default mask (sm). Entries that remain unchanged in the subnet should be defined in an additional template (.subnet31). The name of a template should begin with a dot (.).

Finally, entries are created for each computer. Entries that differ from computer to computer are ha (hardware address) and ip (IP address) which are used for dynamic assignment of IP addresses. The name of an entry is sent to the client as if this has been specified in the hn configuration.

With some DOS clients it may be necessary to specify the additional entry vm rfc1084. By doing so, these clients are presented the answer in a format in compliance with [rfc1084], even if they have made their request in another format. Normally, answers are given in the format which the client has sent the request.

Forless disks that are booted remotely, you can specify where the appropriate boot files can be found. Furthermore, there is some additional data that can be transmitted to a client. An overview of the most important entries is