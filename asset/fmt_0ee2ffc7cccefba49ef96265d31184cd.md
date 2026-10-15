
# ProtocolName

在 `/etc/protocols` 文件中定义的 Internet 协议名称。

- `Wait/NoWait`: 决定 `inet` 守护进程是否等待数据报服务器释放 socket 后继续继续在该 socket 上监听。
- `UserName`: `inet` 应该用于启动服务器的登录用户。
- `ServerPath`: 服务器的完整路径。
- `ServerArgs`: `inet` 应该用于执行服务器的可选命令行参数。

| `ServiceName` | `SocketType` | `ProtocolName` | `Wait/NoWait` | `UserName` | `ServerPath` | `ServerArgs` |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| ftp | stream | tcp | nowait | root | `/usr/bin/ftpd` | ftppd |
| telnet | stream | tcp | nowait | root | `/usr/bin/telnetd` | telnetd |
| shell | | tcp | nowait | root | `/usr/bin/rshd` | rshd |
| login | stream | | | root | `/usr/bin/logind` | rioged |
| exec | stream | tcp | | root | `/usr/bin/rexed` | rexed |
| #uccp | stream | tcp | | root | `/usr/bin/fingerd` | fingered |
| #finger | stream | | nowait | root | `/usr/bin/finger` | fftpd/tmp |
| comsat | dgram | | wait | root | `/usr/bin/comsat` | comsat |
| #talk | dgram | | wait | root | `/usr/bin/talk` | talked |
| ntalk | dgram | | wait | root | `/usr/bin/ntalkd` | ntalkd |

如果你不需要 `ucpd` 的 `wtmp` 条目，则使用用户 `"uccp"`。

`/etc/inetd.conf` 文件不是一个 CDSL，并且由所有集群成员共享。假设你需要禁止某些服务器端应用程序在集群的子成员上执行？例如，假设你只想让一个集群成员执行 ftp 服务（或者替换任何面向网络服务的成员在别名上“加入”）。这并无法通过构建集群别名并让某些成员“加入”该别名来解决。那仅仅限制了特定别名的集群路由和/或服务活动。它并没有说明集群别名成员所提供的服务。这就像买了一张票去看马戏团的狮子，但票给了你一个可以在那里看小丑、杂技演员、大象或任何你想看的东西的地方。

如果你创建一个名为 `cl_ftp_den` 的别名，并希望访问由单个集群成员提供的 ftp 服务，但客户端发出了 `telnet cl_ftp_den` 命令，那么集群别名中没有任何内容是专门用于访问 ftp 服务的。别名只是一个名字。如果所有客户端都遵循名称中隐含的约定（`clu_ftp_den` 应该仅用于 ftp），则该方案将生效。但该方案依赖于所有客户端遵循的约定。

下面的示例显示了由集群中的一个成员“加入”的 `clu_ftp_den` 别名的创建。然后使用该别名加入集群成员，证明了别名对它要激活的服务没有直接控制权。

客户端在一次失败的 ping 尝试未使用不存在的别名。此时，客户端的 `/etc/hosts` 文件已经包含了别名名称和 IP 地址，但别名在集群中不存在。

```
# hostname

# ping clu_ftp_den

PING clu_ftp_den (192.168.0.171): 56 data bytes

---clu_ftp_den PING Statistics---

3 packets transmitted, 0 packets received, 100% packet loss
```

集群成员的 `/etc/hosts` 文件中也反映了别名名称和 IP 地址。

```
# grep /etc/hosts

192.168.0.171 clu_ftp_den
```

在集群成员 `molari` 上创建别名。

```
# /usr/sbin/cluamgr -a alias=clu_ftp_den
# /usr/sbin/cluamgr -s clu_ftp_den

Status of Cluster Alias: clu_ftp_den
netmask: 0
aliasid: 2
flags: ENABLED,IP_4
import_userreserved from net: 0
forwarded: 0
received within cluster: 0
data packets received from network: 0
data packets forwarded within cluster: 0
agrams received from network: 0
agrams forwarded within cluster: 0
agrams received within cluster: 0
fragments received from network: 0
fragments forwarded within cluster: 0
Member Attributes:
memberid: 2, sel=1, rpi=1
```

别名尚未加入，`aliasid` 不感知该别名。让我们纠正这种情况。

```
# /usr/sbin/cluamgr -a alias=clu_ftp_den
# /usr/sbin/cluamgr -s clu_ftp_den

Status of Cluster Alias: clu_ftp_den
netmask: 0
aliasid: 2
flags: ENABLED,IP_4
import_userreserved from net: 0
forwarded: 0
received within cluster: 0
data packets received from network: 0
data packets forwarded within cluster: 0
agrams received from network: 0
agrams forwarded within cluster: 0
agrams received within cluster: 0
fragments received from network: 0
fragments forwarded within cluster: 0
Member Attributes:
memberid: 2, sel=1, rpi=1
```

```
# /usr/sbin/cluamgr -r start

从客户端系统：

# ping clu_ftp_den

PING clu_ftp_den (192.168.0.171): 56 data bytes

64 bytes from 192.168.0.171: icmp_seq=0 ttl=64 time=1 ms
64 bytes from 192.168.0.171: icmp_seq=1 ttl=64 time=0 ms

---clu_ftp_den PING Statistics---

2 packets transmitted, 2 packets received, 0% packet loss

round-trip (ms) min/avg/max = 0/0/1
```

```
# telnet clu_ftp_den

Trying 192.168.0.171...
Connected to clu_ftp_den.
Escape character is '^'.
Compaq True64 UNIX VIX.1A (Rev. 1885) (molari.dec.com) (pts/1)
login: root
# exit

Connection closed by foreign host.
```

集群成员 `sheridan` 不感知 `clu_ftp_den` 别名。

```
# /usr/sbin/cluamgr -s all

Status of Cluster Alias: babylon5.den.com
netmark: 0
aliasid: 1
flags: ENABLE,DEFAULT,IP_4
import_userreserved from net: 5
forwarded: 5
received within cluster: 0
data packets received from network: 1277
```
