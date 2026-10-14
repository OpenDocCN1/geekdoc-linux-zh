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