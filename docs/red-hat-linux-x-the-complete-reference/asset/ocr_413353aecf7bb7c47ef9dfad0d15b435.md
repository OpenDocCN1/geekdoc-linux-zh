```
key myserver {
  algorithm HMAC-MD5;
  secret "CNQAfBBLnvWUSH8hRqq/WA==";
};
```

The key's name can then be used to reference the key in other named statements, such as **allow-update** statements.

```
allow-update myserver;
```

The DNS server or DHCP server with which you are setting up communication will also have to have the same key. See the earlier section "Dynamic Update: DHCP and Journal Files" and Chapter 35 for more information on DHCP and TSIG. For communication between two DNS servers, each would have to have a server statement specifying the shared key. In the following example, the named.conf file for the DNS server on 192.168.0.1 would have to have the following server statement to communicate with the DNS server on 10.0.0.1, using the shared myserver key. The named.conf file on the 10.0.0.1 DNS server would have to have a corresponding server statement for the 192.168.0.1 server.

```
server 10.0.0.1 { keys {myserver;}; };
```