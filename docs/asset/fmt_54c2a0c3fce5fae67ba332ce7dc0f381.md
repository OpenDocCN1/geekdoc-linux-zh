
# -echo stream root internal
# -echo stream udp internal
# -discard stream root internal
# -discard stream udp internal
# -daytime stream root internal
# -daytime stream udp internal
# -chargen stream root internal
# -chargen stream udp internal
# -time stream root internal
# -time stream udp internal

# 这些是标准服务和 BSD 协议。

© Copyright 1999-2000 Gerhard Maurani and Open Network Architecture ®

42

关于本书的意见和建议请邮寄至 `gmourani@videotron.ca`

| Service | Path |
| :--- | :--- |
| `#talk dgram wait root` | `/usr/sbin/tcp in.talkd` |
| `#ntalk dgram wait root` | `/usr/sbin/tcp in.netalkd` |
| `#dtalk stream tcp wait nobody` | `/usr/sbin/tcp in.inetalkd` |

## Pop 和镜像邮件服务所有

| Service | Path |
| :--- | :--- |
| `#pop-2 stream nowait root` | `/usr/sbin/tcp ipop2d` |
| `#pop-3 stream nowait root` | `/usr/sbin/tcp ipop3d` |
| `#imap stream tcp nowait root` | `/usr/sbin/tcp imap4d` |

## Internet UUCP 服务。

| Service | Path |
| :--- | :--- |
| `#uucp stream tcp nowait uucp` | `/usr/sbin/tcp /lib/uucp/uucico` |

## Tftp 服务主要用于托管。大多数站点仅在作为“启动服务器”的机器上运行。除非你需要它，否则不要取消此行的注释。

| Service | Path |
| :--- | :--- |
| `#tftp dgram wait root` | `/usr/sbin/tcp in.tftpd` |
| `#boots dgram wait root` | `/usr/sbin/tcp in.ps` |

## Finger，finger 提供了对潜在黑客有价值的用户信息。许多站点选择禁用部分或全部这些服务以确保安全。

| Service | Path |
| :--- | :--- |
| `#Finger stream tcp nowait root` | `/usr/sbin/tcp in.fingerd` |
| `#clinger stream tcp nowait root` | `/usr/sbin/tcp in.fingerd` |
| `#sysstat stream tcp nowait guest` | `/usr/sbin/tcp /bin/ps -auxx` |
| `#netstat stream tcp nowait guest` | `/usr/sbin/tcp /bin/inetstat -f` |

## 认证

| Service | Path |
| :--- | :--- |
| `#auth stream tcp nowait nobody` | `/usr/sbin/in.ident in.inetd -le` |

# inetd.conf 结束

注意：在修改 `inetd.conf` 文件后，别忘记向 `inetd` 发送 `SIGHUP` 信号（`kill -HUP inetd`）。

## 第 4 步

采取的一种保护 "`inetd.conf`" 文件的安全措施是使用 `chatter` 命令将其设置为不可修改。

### 要设置文件为不可修改，执行以下命令：
```
[root@deep]# chatter +i/etc/inetd.conf
```

这将防止对 "`inetd.conf`" 文件进行任何（意外或其他）的更改。具有不可修改属性“i”的文件不能被修改、删除或重命名，无法为该文件创建链接，也无法向其中写入数据。只有超级用户 `root` 可以设置或清除此属性。

如果你想修改 `inetd.conf` 文件，将需要先取消不可修改标记：

### 要取消不可修改标记，只需执行以下命令：

关于此书的意见和建议请邮寄至 `gmourani@videotron.ca`

```bash
[root@deep ~]# 채팅 -i /etc/inetcd.conf
```

## 11. TCP_WRAPPERS

Red Hat Linux 允许所有服务请求。使用 `TCP_WRAPPERS` 保护服务器免受外部入侵比你想象的要简单且轻松。通过在 `/etc/hosts.deny` 中设置 '`ALL: ALL@ALL, PARANOID`' 来拒绝所有主机，并在 `/etc/hosts.allow` 文件中显式列出允许访问机器的信任主机是最安全且最好的配置。

`TCP_WRAPPERS` 由两个文件控制，搜索会在第一个匹配项处停止。

`/etc/hosts.allow`
`/etc/hosts.deny`

- 当 (守护进程，客户端) 对匹配 `/etc/hosts.allow` 文件中的条目时，将授予访问。
- 否则，当 (守护进程，客户端) 对匹配 `/etc/hosts.deny` 文件中的条目时，将拒绝访问。
- 否则，将授予访问。

### 第 1 步

编辑 `hosts.deny` 文件 (`vi /etc/hosts.deny`) 并添加以下行：

```
# 默认拒绝访问。
# 拒绝所有人的访问。
ALL: ALL@ALL, PARANOID # 匹配名称与其地址不符的主机，见下文。
```

这意味着所有服务，因此任何未显式允许的服务都会被拦截，除非它们被允许文件中的条目许可。

> **注意：** 使用参数 "`PARANOID`"；如果你打算在服务器上使用 `telnet` 或 `ftp` 服务，别忘记在服务器的 `/etc/hosts` 文件中添加客户端机器名和 IP 地址，否则你可能需要等待几分钟直到 DNS 查询超时，才能看到登录提示。

### 第 2 步

编辑 `hosts.allow` 文件 (`vi /etc/hosts.allow`) 并添加例如以下行：

显式的主机在允许文件中列出。例如：

```
sshd: 208.164.186.1 gate.openarch.com
```

对于你的客户端机器：`208.164.186.1` 是 IP 地址，`gate.openarch.com` 是允许使用 `sshd` 的客户端之一的主机名。

### 第 3 步

`tcpdchk` 程序是 `tcp wrapper` 配置检查器。它检查你的 `tcp wrapper` 配置并报告它能找到的所有实际问题。

- 完成配置后，运行程序 `tcpdchk`。

```bash
[root@deep ~]# tcpdchk
```
