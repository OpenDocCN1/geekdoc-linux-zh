
$TCIP-INFO, amge $SYSSYSTEM:`TCPIP$SMTP_RECEIVER.EXE` 已安装

$TCIP-INFO, 逻辑名称已创建

$TCIP-INFO, 服务队列已启动

$TCIP-INFO, 服务已启用

$TCIP-S-STARTDONE, `TCPIP$SMTP` 启动完成

按回键继续...

![](img/3ba916f144e94350147c366c3485e02e_77_0.png)

## OpenVMS 组件 Compaq TCP/IP 服务配置菜单

配置选项：

| 1 | FTP | 已启用 启动 |
| 2 | NFS Client | 已禁用 停止 |
| 3 | EXEC and RSH | 已禁用 停止 |
| 4 | LOGIN | 已启用 启动 |
| 5 | SMTP | 已启用 启动 |
| 6 | TELNET | 已启用 启动 |
| 7 | DMCP | 已禁用 停止 |
| 8 | Telnetsys | 已禁用 停止 |

A - 配置选项 1 - 8

[E] - 退出菜单

输入配置选项: `e`

![](img/3ba916f144e94350147c366c3485e02e_77_1.png)

## OpenVMS Compaq TCP/IP 服务配置菜单

配置选项：

- 核心环境
- 客户端组件
- 服务器组件
- 可选组件
- 关闭 OpenVMS Compaq TCP/IP 服务
- 启动 OpenVMS Compaq TCP/IP 服务
- 运行测试
- 配置选项 1 - 4
- 退出配置程序

输入配置选项: `3`

6-7 选择 服务器组件 菜单选项。

## OpenVMS Compaq TCP/IP 服务服务器组件配置菜单

配置选项：

1 - BIND 已禁用 停止
2 - BOOT 已禁用 停止
3 - DHCP 已禁用 停止
4 - FINGER 已禁用 停止
5 - FTP 已启用 启动
6 - IMAP 已禁用 停止
7 - LBRKER 已禁用 停止
8 - L/PD 已启用 启动
9 - METRIC 已禁用 停止
10 - NFS 已禁用 停止
11 - LOCKD/STAT 已禁用 停止
12 - MTP 已禁用 停止
13 - PC-HFS 已禁用 停止
14 - POP 已禁用 停止
15 - POPMAPPER 已启用 启动
16 - LOGIN 已启用 启动
17 - RMT 已禁用 停止
18 - SNMP 已禁用 停止
19 - TELNET 已启用 启动
20 - TFTP 已禁用 停止
21 - XDM 已禁用 停止

- 配置选项 1 - 21
- 退出菜单

输入配置选项: `6`

6-8 选择要配置 IMAP 协议。

### IMAP 配置

服务定义在 `SYSUAF` 中。

服务定义在 `TCPIP$SERVICE` 数据库中。

服务未启用。

服务已停止。

IMAP 配置选项：

- 在所有节点上启用服务
- 在此节点上启用服务
- 在此节点上启用并启动服务

> [E] 退出 IMAP 配置

输入配置选项: `3`

图 6-9 选择 3 以激活并启动此 OpenVMS 系统的 IMAP 服务。

### IMAP 配置

服务定义在 `SYSUAF` 中。

服务定义在 `TCPIP$SERVICE` 数据库中。

服务未启用。

服务已停止。

IMAP 配置选项：

- 在所有节点上启用服务
- 在此节点上启用服务
- 在此节点上启用并启动服务

> [E] 退出 IMAP 配置

输入配置选项: `3`

```
输入配置选项: 3
%TCPIP-I-INFO, image SYS$SYSTEM:TCPIP$IMAP_SERVER.EXE 已安装
%TCPIP-I-INFO, 服务已启用
%TCPIP-S-STARTUP, TCPIP$IMAP 启动完成
按回键继续 ...
```

图 6-10 退出并返回 TCP/IP 主菜单。

## OpenVMS Compaq TCP/IP 服务服务器组件配置菜单

配置选项：

| 1 - BIND | 已禁用 停止 | 12 - HTTP | 已禁用 停止 |
| 2 - BOOTP | 已禁用 停止 | 13 - PC-NFS | 已禁用 停止 |
| 3 - DHCP | 已禁用 停止 | 14 - POP | 已禁用 停止 |
| 4 - FINGER | 已禁用 停止 | 15 - PORTMAPPER | 已禁用 停止 |
| 5 - FTP | 已启用 启动 | 16 - RLOGIN | 已启用 启动 |
| 6 - IMAP | 已启用 启动 | 17 - RMQ | 已禁用 停止 |
| 7 - LOKER | 已禁用 停止 | 18 - SNMP | 已禁用 停止 |
| 8 - LPF/LFD | 已禁用 停止 | 19 - TELNET | 已启用 启动 |
| 9 - METRIC | 已禁用 停止 | 20 - TFTP | 已禁用 停止 |
| 10 - NFS | 已禁用 停止 | 21 - XDM | 已禁用 停止 |
| 11 - LOCKD/STAT | 已禁用 停止 | | |

A - 配置选项 1 - 21

[E] 退出菜单

输入配置选项:

图 6-11 注意 IMAP 服务现在已在该系统上启用并启动。

## OpenVMS Compaq TCP/IP 服务服务器组件配置菜单

配置选项：

| 1 - BIND | 已禁用 停止 | 12 - HTTP | 已禁用 停止 |
| 2 - BOOTP | 已禁用 停止 | 13 - PC-NFS | 已禁用 停止 |
| 3 - DHCP | 已禁用 停止 | 14 - POP | 已禁用 停止 |
| 4 - FINGER | 已禁用 停止 | 15 - PORTMAPPER | 已禁用 停止 |
| 5 - FTP | 已启用 启动 | 16 - RLOGIN | 已启用 启动 |
| 6 - IMAP | 已启用 启动 | 17 - RMQ | 已禁用 停止 |
| 7 - LOKER | 已禁用 停止 | 18 - SNMP | 已禁用 停止 |
| 8 - LPF/LFD | 已禁用 停止 | 19 - TELNET | 已启用 启动 |
| 9 - METRIC | 已禁用 停止 | 20 - TFTP | 已禁用 停止 |
| 10 - NFS | 已禁用 停止 | 21 - XDM | 已禁用 停止 |
| 11 - LOCKD/STAT | 已禁用 停止 | | |

A - 配置选项 1 - 21

[E] 退出菜单

输入配置选项: `14`

图 6-12 选择 POP 协议。OpenVMS 兼容性

### POP 配置

服务定义在 `SYSUAF` 中。

服务定义在 `TCPIP$SERVICE` 数据库中。

服务 启用。

POP 配置选项：

- 在所有节点上启用服务
- 在此节点上启用服务
- 在此节点上启用并启动服务

[E] 退出配置

输入配置选项: `3`

![](img/3ba916f144e94350147c366c3485e02e_81_0)

### POP 配置

服务定义在 `SYSUAF` 中。

服务定义在 `TCPIP$SERVICE` 数据库中。

服务未启用。

服务已停止。

POP 配置选项：

- 在所有节点上启用服务
- 在此节点上启用服务
- 在此节点上启用并启动服务

[E] 退出配置

```
输入配置选项: 3
%TCPIP-I-INFO, image SYS$SYSTEM:TCPIP$POP.EXE 已安装
%TCPIP-I-INFO, 服务已启用
%TCPIP-S-STARTUP, TCPIP$POP 启动完成
按回键继续...
```

![](img/3ba916f144e94350147c366c3485e02e_81_1)

## OpenVMS Compaq TCP/IP 服务服务器组件菜单

配置选项：

| 1 - BIND | 已禁用 停止 | 12 - NTP | 已禁用 停止 |
| 2 - BOOTP | 已禁用 停止 | 13 - PC-NFS | 已禁用 停止 |
| 3 - DHCP | 已禁用 停止 | 14 - POP | 已启用 启动 |
| 4 - FINGER | 已禁用 停止 | 15 - PORTMAPPER | 已禁用 停止 |
| 5 - FTP | 已启用 启动 | 16 - RLOGIN | 已启用 启动 |
| 6 - IMAP | 已启用 启动 | 17 - RMT | 已禁用 停止 |
| 7 - LBROKER | 已禁用 停止 | 18 - SNMP | 已禁用 停止 |
| 8 - LPR/LPD | 已禁用 停止 | 19 - TELNET | 已启用 启动 |
| 9 - METRIC | 已禁用 停止 | 20 - TFTP | 已禁用 停止 |
| 10 - NFS | 已禁用 停止 | 21 - XDM | 已禁用 停止 |
| 11 - LOCK/STATD | 已禁用 停止 | | |

A - 配置选项 1 - 21
