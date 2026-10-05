Matches any host on an IPv4 network for which the system has an interface.

The localhost and localnets ACLs do not currently support IPv6 (that is, localhost does not match the host's IPv6 addresses, and localnets does not match the host's attached IPv6 networks) due to the lack of a standard method of determining the complete set of local IPv6 addresses for a host.

# 6.2.3. controls Statement Grammar

```
controls {
  inet ( ip_addr | * ) [ ip_port ] allow { address_match_list }
    keys [ key_list ];

  inet ...;
}
```

# 6.2.4. controls Statement Definition and Usage

The controls statement declares channels used by system administrators to affect the operation of the local nameserver. These channels are created by the rnd utility to send commands and retrieve non-DNS results from a nameserver.

An inet control is a TCP socket listening at the specified ip_port on the specified ip_addr, which can be an IPv4 or IPv6 address. An ip_addr of * is interpreted as the IPv4 wildcard addresses; connections will be accepted on any of the system's IPv4 addresses. To listen on the IPv6 wildcard address, use an ip_addr of ::. If you will use rnd on the local host, using the loopback address (127.0.0.1 or ::1) is recommended for maximum security.

The ability to issue controls over the control channel is restricted by the allow and keys clauses. Connections to the control channel are permitted based on the address permissions in address_match_list, key_id members of address_match_list are listed, and instead independently interpreted based on the key_list. Each key id in the key_list is allowed to be used to authenticate commands and responses over the control channel by digitally signing each message between the server and a command client (See Remote Name Daemon Control application in Section 3.4.1.2). All commands to the control channel must be signed by one of its specified keys to be honored.