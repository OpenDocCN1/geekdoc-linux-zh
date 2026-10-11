
`root[1]-# smbgetserverinfo -v -i 10.0.0.13`

ERROR: SMBTC createAndX()

10.0.0.13 的服务器信息

Server Name : *SMBSERVER

Server OS : Windows 5.1

Workgroup/Domain : WORKGROUP

`root[1]-# smbgetserverinfo -v -i 10.0.0.10`

10.0.0.10 的服务器信息

Server Name : SERVER

Server OS : Unix

Workgroup/Domain : HOMELAN

`root[1]-# | | |`

通过空会话（null session）连接到 Samba 服务器，你可以获取 Samba 名称和操作系统版本。`smbdumpers` 程序可以显示如图 3.18 所示更多信息。尽管 Windows XP 目标没有返回任何信息，但 Linux 目标返回了所有本地用户列表，尽管没有显示 `aaron` 的本地 Samba 账户。虽然这些工具对旧环境可能有用，但在攻击新的 Windows 环境时，应该使用 `nbtscan` 和 `Nessus` 等其他工具。

# 第 3 章 • 网络的枚举与扫描

## 图 3.18 smbdumpusers 示例

| 会话 编辑 查看 签签 设置 帮助 |

|---||

| `root[#] smbdumpusers -1 10.0.0.13`

ERROR: SMBNTCreateAndX())

ERROR: SMBNTCreatatAndX())

`root[#] smbdumpusers -1 10.0.0.10`

Administrator

nbody

Domain Admins

Domain Users

Domain Guests

root

bin

bin

daemon

adm

sys

lp

adm

sync

tty

shutdown

disk

halt

lp

mail

mem

news

known

uuucp

uucp

wheel

operator

games

mail

gosher

news

ftp

uucp

mail

floppy

games

slocate

utmp Shell |

## xSMBBrowser

如果发现目标存在 SMB，你需要尝试获取更多关于所提供共享的信息。`xSMBBrowser` 提供了一个 GUI 环境，用于连接和枚举组内或域内的系统。启动 `xSMBBrowser`，并选择 Samba Config 以开始浏览。它将执行 `nmlookup` 来搜索工作组/域，返回的任何系统将通过 `smbclient` 运行，以列出并连接远程共享。根据目标系统的安全设置，你将能够查看和浏览共享，如图 3.19 所示。

## 图 3.19 xSMBBrowser 查找与枚举

![](img/b38c01d2fda8509e8449e32f876ae148_129_0.png)

## smbclient

如果你正在枚举一个目标并确定有一个可访问的文件共享，你如何访问它来检索或发送文件呢？最旧的方法之一是使用 `smbclient`，它是一个用于 SMB 网络的文件传输客户端，工作方式类似于 FTP 客户端。使用 `-U` 参数并使用 `-I` 指定目标主机。图 3.20 显示了使用 `smbclient` 成功连接到目标系统，用于发送后续可能在渗透测试中使用的文件。

# 第 3 章 · 网络的枚举与扫描

## 图 3.20 smbclient 发送文件

```
Shell - Net utils
会话 编辑 查看 签签 设置 帮助
root@[kno]# smbclient -I 192.168.1.1 -U Administrator\\192.168.1.1\$
Password:
Domain:[NYYPDC1] OS:[Windows 5.0] Server:[Windows LAN Manager]
smb:\> cd system32
smb:\winnt> cd system32
smb:\winnt\system32> put /tmp/trojan.exe
put /tmp/trojan.exe as \winnt\system32\RUNME.EXE (0.0 kb/s) (0.0 kb/s)
smb:\winnt\system32>
```

## 总结

在本章中，我们介绍了许多工具，以及这些工具不同的开关/参数。表 3.2 列出了这里提到的所有工具、使用的开关及其预期用途。

| 工具 | 开关 | 预期用途 |
|---|---|---|
| `tee` | `-a` | 追加写入文件 |
| `nmap` | `-sp` | 使用 ICMP 和 TCP ACK (root) 扫描 |
| | `-P0` | 在扫描前进行 ICMP ping |
| | `-PS` | 使用 TCP ACK 作为探测 |
| | `-PP` | 使用 ICMP 时间戳探测 |
| | `-PM` | 使用 ICMP 掩码探测 |
| | `-oA` | 输出所有类型的日志、标准文本、XML 和可 grep 文件 |
| | `--resumefile` | 恢复之前取消的 nmap 扫描 |
| | `-sT` | 基于连接的扫描，默认用户权限 |
| | `-sS` | SYN 扫描，默认 root 权限 |
| | `-b` | 从服务器跳跃扫描 |
| | `@server:ftpport` | |

# 表 3.2 工具、开关与用途（续）

| 工具 | 开关 | 预期用途 |
|---|---|---|
| `-` | `-` | |
| | `-sl zombiehost:port` | 空空主机扫描 |
| | `-O` | 使用操作系统指纹识别 |
| | `-IL hostfile` | 使用主机列表作为目标列表 |
| | `-T[0,1,2,3,4,5]` | 设置扫描计时，从谨慎 (T0) 到疯狂 (TS) |
| | `-p[ports]/portlist/port1-port2]` | 扫描 [ports]/portlist/port1-port2] |
| | `-p[ports]/portlist/port1-port2]` | 扫描 [ports]/portlist/port1-port2] |
| | `-p[ports]/portlist/port1-port2]` | 扫描 [ports]/portlist/port1-port2] |
| | `-p[ports]/portlist/port1-port2]` | 扫描 [ports]/portlist/port1-port2] |
| | `-p[ports]/portlist/port1-port2]` | 扫描 [ports]/portlist/port1-port2] |
| | `-p[ports]/portlist/port1-port2]` | 扫描 [ports]/portlist/port1-port2] |
| | `-p[ports]/portlist/port1-port2]` | 扫描 [ports]/portlist/port1-port2] |
| | `-p[ports]/portlist/port1-port2]` | 扫描 [ports]/portlist/port1-port2] |
| | `-p[ports]/portlist/port1-port2]` | 扫描 [ports]/portlist/port1-port2] |
| | `-p[ports]/portlist/port1-port2]` | 扫描 [ports]/portlist/port1-port2] |
| | `-p[ports]/portlist/port1-port2]` | 扫描 [ports]/portlist/port1-port2] |
| | `-p[ports]/portlist/port1-port2]` | 扫描 [ports]/portlist/port1-port2] |
| | `-p[ports]/portlist/port1-port2]` | 扫描 [ports]/portlist/port1-port2] |
| | `-p[ports]/portlist/port1-port2]` | 扫描 [ports]/portlist/port1-port2] |
| | `-p[ports]/portlist/port1-port2]` | 扫描 [ports]/portlist/port1-port2] |
| | `-p[ports]/portlist/port1-port2]` | 扫描 [ports]/portlist/port1-port2] |
