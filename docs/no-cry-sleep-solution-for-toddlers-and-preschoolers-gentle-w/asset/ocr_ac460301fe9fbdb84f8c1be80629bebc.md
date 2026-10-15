can also add or remove items from these lists with the += and -= operators. Use += to add values and -= to remove values. You often use the += and -= operators to add values to attributes that may have an initial value assigned in the default block.

Attributes are listed in Table 20-6. Certain attributes are required for a service. These include socket_type and wait. For a standard Internet service, you also need to provide the user (user ID for the service), the server (name of the server program), and the protocol (protocol used by the server). With server_args, you can also list any arguments you want passed to the server program (this does not include the server name as with tcpd). If protocol is not defined, the default protocol for the service is used.

```
service tftp
{
    socket_type = stream
    wait = no
    user = root
    protocol = ftp
    server = /usr/sbin/in.tftpd
    server_args = -l -a
    disable = yes
}
```

# TABLE 20-6
xinetd Attributes

| Attribute | Description |
|---|---|
| id | Identifies a service. By default, the service ID is the same as the service name. |
| type | Type of service: RPC, INTERNAL (provided by xinetd), or UNLISTED (not listed in a standard system file). |
| flags | Possible flags include REUSE, INTERCEPT, NORETRY, IDONLY, NAMEINARGS (allows use of tcpd), NODELAY, and DISABLE (disable the service). See the xinetd.conf man page for more details. |
| disable | Specify yes to disable the service. |
| socket_type | Specify stream for a stream-based service, dgram for a datagram-based service, raw for a service that requires direct access to IP, and seqpacket for reliable sequential datagram transmission. |
| protocol | Specifies a protocol for the service. The protocol must exist in /etc/protocols. If this attribute is not defined, the default protocol employed by the service will be used. |