# CHOKE SSH CONFIGURATION

The first rule allows local connections from the choke machine to sshd servers running in the DMZ, including the gateway firewall host:

```
$IPT -A OUTPUT -o SDM2_INTERFACE -p tcp \
-S SDM2_IPADDR --sport SUNPRIVPORTS \
-d SDM2_ADDRESSES --port 22 \
-m state --state NEW -j ACCEPT
```

The next rule forwards connections from LAN clients to any remote server:

```
$IPT -A FORWARD -i SLAN_INTERFACE -o SDM2_INTERFACE -p tcp \
-S SLAN_ADDRESSES --sport SUNPRIVPORTS --port 22 \
-m state --state NEW -j ACCEPT
```

The last rule forwards connections from a selected remote client address to a specific local host, which, in this case, resides in the LAN:

```
$IPT -A FORWARD -i SDM2_INTERFACE -o SLAN_INTERFACE -p tcp \
-s <selected remote host> --sport SUNPRIVPORTS \
-d <selected LAN host> --port 22 \
-m state --state NEW -j ACCEPT
```

# FTP (TCP Ports 21 and 20)

FTP has two modes for exchanging data between a client and a server: normal data channel port mode and passive data channel mode. Port mode is the default mechanism when using the FTP client program and connecting to a remote FTP site. Passive mode is the mechanism used when connecting to an FTP site through a web browser. Occasionally, you might encounter an FTP site that supports only one mode.

Two approaches to client and server FTP combinations are described in this section:

+   - The gateway is simply a gateway to remote FTP servers; the choke machine and the LAN hosts are clients.
+   
+   - An FTP server runs in the DMZ; the choke, LAN hosts, and remote hosts are clients.

# GATEWAY AS CONDUIT TO REMOTE FTP SERVERS

It’s almost a given that most sites will want FTP client access to remote file repositories. The first section allows internal hosts to connect to remote FTP servers.

The following rules allow outgoing FTP client connections from the choke host and the LAN machines. The constants are those used on the gateway: