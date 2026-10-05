

# 从命令行安装打印机驱动程序

正如你可能猜到的那样，没有 Windows 的话，某些步骤是很难复制的，特别是设置打印机默认值。但如果你想在 Samba 服务器上设置数百台打印机，你可能想一直尝试从命令行进行操作。命令行配置对于 PostScript 打印机特别有效，因为 Windows PostScript 打印机驱动程序在没有默认配置信息的情况下也能工作。

如果你记录了特定驱动程序所需的文件，就可以从命令行安装驱动程序。首先，将所需的文件复制到 [print]$ 共享目录：

```
$ cd ~/mydriver
$ smclient -U printdam //samba-server/print$ -c "mput *"
```

接下来，将驱动程序分配给特定的打印机。假设你有一个带有自定义 PPD 文件的简单 Post-Script 打印机：

```
$ rpclient -U printdam -c "\"
addriver\"Windows NT x86\"Our Custom PS:\nPSCRIPT.DLL:CUSTOM.PPD:PSSUI.DLL:PSCRIPT.HLP:NULL:NULL:PSCRIPT.NTF""\nsamba-server
```

行末的反斜杠允许命令拆分成多行以保持清晰；如果你愿意，可以省略它们并在单行中输入命令。双引号前的反斜杠用于区分嵌套的引号集。

上述示例中的长字符串包含了在 Windows 安装打印机驱动程序时看到的驱动程序属性中列出的信息：

- 长打印名称
- 驱动程序文件名
- 数据文件名
- 配置文件名
- 帮助文件名
- 语言监控名称（如果没有，则将其设置为 NULL）
- 默认数据类型（如果没有，则将其设置为 NULL）
- 逗号分隔的附加文件列表

要配置打印机使用已上传的驱动程序之一：

```
$ rpclient -U printdam -c "\"Our Custom PS\"" samba-server
```

# 30.8 调试 SAMBA

Samba 通常在运行时不需要不需要太多关注。然而，如果你遇到问题，可以查阅两个主要的调试信息源：每个客户端的日志文件和 smbstatus 命令。确保你的配置文件中有恰当的日志设置。

```
[global]
: %m 为每个客户端写入一个单独的文件。
log file = /var/log/samba.log.%m
max size = 1000
: 记录多少信息。你也可以为系统组件指定日志级别（这里通常为 3，认证级别为 10）。
log level = 3 auth:10
```

较高的日志级别会产生更多信息。记录日志需要时间，除非你正在进行调试，否则不要请求过多的细节。操作可能会显著变慢。

以下示例显示了失败内容后跟随成功内容所生成的日志。

```
2009/09/05 16:29:45, 2] auth/auth.c.check_ntlm_password(312)
check_ntlm_password: Authentication for user [oetiker] -> [oetiker] FAILED
with ERROR_STATUS_WRONG_PASSWORD
2009/09/05 16:29:45, 2] smbd/server.c.exit_server(571)
Closing connections
2009/09/05 16:29:57, 2] auth/auth.c.check_ntlm_password(305)
check_ntlm_password: authentication for user [oetiker] -> [oetiker]
[oetiker] succeeded
2009/09/05 16:29:57, 1] smbd/service.c.make_connection_snum(648)
ets(127.0.0.1) connect to service oetiker initially as user oetiker
(uid=1000, gid=1000) (pid 2042)
2009/09/05 16:29:58, 1] smbd/service.c.close_cnum(837)
etsuko(127.0.0.1) closed connection to service oetiker
2009/09/05 16:29:58, 2] smbd/server.c.exit_server(571)
Closing connections
```

smbdcontrol 方便于在不修改 smb.conf 的情况下更改运行中的 Samba 服务器上的调试级别。例如：

```
$ sudo smbdcontrol debug "4 auth:10"
```

上述示例将全局调试级别设置为 4，并将认证相关事务的调试级别设置为 10。smbd 参数指定系统上所有 smb 守护进程都将设置其调试。要调试特定的已建立连接，可以使用 smbstatus 命令确定哪个 smb 守护进程处理该连接，并将 PID 传递给 smbd debug 仅一个连接。在日志级别超过 100 时，你将会在日志中看到（加密的）密码。

smbstatus 显示当前活动的连接和锁文件。这些信息在你追踪锁定问题时（例如，“哪个用户打开了文件 xyz 进行独占读/写？”））特别有用。输出的第一部分列出了用户连接的资源。最后部分列出了任何文件锁。

# 第 30 章与 Windows 协调

```
$ sudo smbstatus # 为了清晰起见，压缩了一些输出行
```
Samba 版本 3.4.1

| PID | Username | Group | Machine |
|---|---|---|---|
| 10612 | trent | atrust | tan (192.168.0.6) |
| 5283 | ned | atrust | ithaca (192.168.0.1) |
| 1037 | paul | atrust | pauldesk2 (192.168.0.48) |
| 8137 | trent | atrust | atlantic (192.168.1.3) |
| 1173 | jim | jim | jim-desktop (192.168.0.7) |
| 11563 | mgetty | mickey | mgetty (192.168.0.5) |
| 6125 | brian | brian | brian-desktop (192.168.0.16) |

| Service | pid | machine | Connected at |
|---|---|---|---|
| swdepot2 | 18335 | john-desktop | Thu 15:40 |
| goldmine | 1173 | jim-desktop | Thu 15:38 |
| swdepot2 | 1037 | pauldesk2 | Tue 08:59 |
| admin | 1037 | pauldesk2 | Tue 08:59 |
| swdepot2 | 6125 | brian-desktop | Fri 12:21 |
| swdepot2 | 11563 | mgetty | Fri 12:47 |

| PID | DenyMode | Access R/W | Name |
|---|---|---|---|
| 1037 | DENY_WRITE 0x208 | RDONLY | /home/paul/ |
| 6125 | DENY_WRITE 0x219 | RDWR | /home/trent/ |
| 1037 | DENY_WRITE 0x219 | RDWR | /home/sam/ |
| 18335 | DENY_WRITE 0x219 | RDWR | /home/ben/ |

# 30.9 活跃 Directory 认证

Samba 通常在运行期间不需要太多关注。然而，如果你遇到问题，可以查阅两个主要的调试信息源：每个客户端的日志文件和 smbstatus 命令。确保你的配置文件中有恰当的日志设置。

```
[global]
: %m 为每个客户端写入一个单独的文件。
log file = /var/log/samba.log.%m
max size = 1000
: 记录多少信息。你也可以为系统组件指定日志级别
（这里通常为 3，认证级别为 10）。
log level = 3 auth:10
```

较高的日志级别会产生更多信息。记录日志需要时间，除非你正在进行调试，否则不要请求过多的细节。操作可能会显著变慢。

以下示例显示了失败内容后跟随成功内容所生成的日志。

```
2009/09/05 16:29:45, 2] auth/auth.c.check_ntlm_password(312)
check_ntlm_password: Authentication for user [oetiker] -> [oetiker] FAILED
with ERROR_STATUS_WRONG_PASSWORD
2009/09/05 16:29:45, 2] smbd/server.c.exit_server(571)
Closing connections
2009/09/05 16:29:57, 2] auth/auth.c.check_ntlm_password(305)
check_ntlm_password: authentication for user [oetiker] -> [oetiker]
[oetiker] succeeded
2009/09/05 16:29:57, 1] smbd/service.c.make_connection_snum(648)
ets(127.0.0.1) connect to service oetiker initially as user oetiker
(uid=1000, gid=1000) (pid 2042)
2009/09/05 16:29:58, 1] smbd/service.c.close_cnum(837)
etsuko(127.0.0.1) closed connection to service oetiker
2009/09/05 16:29:58, 2] smbd/server.c.exit_server(571)
Closing connections
```

smbdcontrol 方便于在不修改 smb.conf 的情况下更改运行中的 Samba 服务器上的调试级别。例如：

```
$ sudo smbdcontrol debug "4 auth:10"
```

上述示例将全局调试级别设置为 4，并将认证相关事务的调试级别设置为 10。smbd 参数指定系统上所有 smb 守护进程都将设置其调试。要调试特定的已建立连接，你可以使用 smbstatus 命令确定哪个 smb 守护进程处理该连接，并将 PID 传递给 smbd debug 仅一个连接。在日志级别超过 100 时，你将会在日志中看到（加密的）密码。

smbstatus 显示当前活动的连接和锁文件。这些信息在你追踪锁定问题时（例如，“哪个用户打开了文件 xyz 进行独占读/写？”）特别有用。输出的第一部分列出了用户连接的资源。最后部分列出了任何文件锁。

# 第 30 章 与 Windows 协调

```
$ sudo smbstatus # 为了清晰起见，压缩了一些输出行
```
Samba 版本 3.4.1

| PID | Username | Group | Machine |
|---|---|---|---|
| 10612 | trent | atrust | tan (192.168.0.6) |
| 5283 | ned | atrust | ithaca (192.168.0.1) |
| 1037 | paul | atrust | pauldesk2 (192.168.0.48) |
| 8137 | trent | atrust | atlantic (192.168.1.3) |
| 1173 | jim | jim | jim-desktop (192.168.0.7) |
| 11563 | mgetty | mickey | mgetty (192.168.0.5) |
| 6125 | brian | brian | brian-desktop (192.168.0.16) |

| Service | pid | machine | Connected at |
|---|---|---|---|
| swdepot2 | 18335 | john-desktop | Thu 15:40 |
| goldmine | 1173 | jim-desktop | Thu 15:38 |
| swdepot2 | 1037 | pauldesk2 | Tue 08:59 |
| admin | 1037 | pauldesk2 | Tue 08:59 |
| swdepot2 | 6125 | brian-desktop | Fri 12:21 |
| swdepot2 | 11563 | mgetty | Fri 12:47 |

| PID | DenyMode | Access R/W | Name |
|---|---|---|---|
| 1037 | DENY_WRITE 0x208 | RDONLY | /home/paul/ |
| 6125 | DENY_WRITE 0x219 | RDWR | /home/trent/ |
| 1037 | DENY_WRITE 0x219 | RDWR | /home/sam/ |
| 18335 | DENY_WRITE 0x219 | RDWR | /home/ben/ |

# 30.9 活跃 Directory 认证

Samba 通常在运行期间不需要太多关注。然而，如果你遇到问题，可以查阅两个主要的调试信息源：每个客户端的日志文件和 smbstatus 命令。确保你的配置文件中有恰当的日志设置。

```
[global]
: %m 为每个客户端写入一个单独的文件。
log file = /var/log/samba.log.%m
max size = 1000
: 记录多少信息。你也可以为系统组件指定日志级别
（这里通常为 3，认证级别为 10）。
log level = 3 auth:10
```

较高的日志级别会产生更多信息。记录日志需要时间，除非你正在进行调试，否则不要请求过多的细节。操作可能会显著变慢。

以下示例显示了失败内容后跟随成功内容所生成的日志。

```
2009/09/05 16:29:45, 2] auth/auth.c.check_ntlm_password(312)
check_ntlm_password: Authentication for user [oetiker] -> [oetiker] FAILED
with ERROR_STATUS_WRONG_PASSWORD
2009/09/05 16:29:45, 2] smbd/server.c.exit_server(571)
Closing connections
2009/09/05 16:29:57, 2] auth/auth.c.check_ntlm_password(305)
check_ntlm_password: authentication for user [oetiker] -> [oetiker]
[oetiker] succeeded
2009/09/05 16:29:57, 1] smbd/service.c.make_connection_snum(648)
ets(127.0.0.1) connect to service oetiker initially as user oetiker
(uid=1000, gid=1000) (pid 2042)
2009/09/05 16:29:58, 1] smbd/service.c.close_cnum(837)
etsuko(127.0.0.1) closed connection to service oetiker
2009/09/05 16:29:58, 2] smbd/server.c.exit_server(571)
Closing connections
```

smbdcontrol 方便于在不修改 smb.conf 的情况下更改运行中的 Samba 服务器上的调试级别。例如：

```
$ sudo smbdcontrol debug "4 auth:10"
```

上述示例将全局调试级别设置为 4，并将认证相关事务的调试级别设置为 10。smbd 参数指定系统上所有 smb 守护进程都将设置其调试。要调试特定的已建立连接，你可以使用 smbstatus 命令确定哪个 smb 守护进程处理该连接，并将 PID 传递给 smbd debug 仅一个连接。在日志级别超过 100 时，你将会在日志中看到（加密的）密码。

smbstatus 显示当前活动的连接和锁文件。这些信息在你追踪锁定问题时（例如，“哪个用户打开了文件 xyz 进行独占读/写？”）特别有用。输出的第一部分列出了用户连接的资源。最后部分列出了任何文件锁。

# 活跃 Directory 认证

Windows 桌面大多可能使用 Microsoft 的 Active Directory 进行认证、目录服务和其他网络服务。Active Directory (AD) 将用户、组、计算机和操作系统整合到一个伞下，集中并简化了系统管理。这也是 Windows 在许多企业中立足的主要原因之一。UNIX 汇集了该拼图的一些碎片，但没有任何 UNIX 解决方案像 Active Directory 那样完善或被广泛实施。借助 Samba 的帮助，Linux 系统可以加入 Active Directory 域，并允许在 /etc/passwd 中没有定义的账户访问系统。Linux UID 派自其对应的 Windows 用户，即安全标识符 SID。通过利用 PAM，可以为没有家目录的用户自动创建。所有这些 Windows 集成魔法都由 Samba 中名为 winbind 的组件处理。集成甚至允许 passwd 命令更改用户的 AD 密码。

# 准备 Active Directory 集成

参见第 908 页获取关于 PAM 信息。长期以来，Samba 项目在为 UNIX 和 Linux 提供 Active Directory 支持方面取得了巨大进展。借助 Samba 的帮助，Linux 系统可以加入 Active Directory 域，并允许在 /etc/passwd 中没有定义的账户访问系统。

在你的 Linux 系统进入 Active Directory 天堂之前，你必须完成以下配置任务：

- 安装支持 Active Directory 和身份转换的 Samba。
- 配置命名服务切换 nss.conf，使用 winbind 作为用户、组和密码信息的源。
- 配置 PAM 通过 winbind 进行认证请求。
- 配置 Active Directory 为 Kerberos 区域。

参见第 17 章获取关于 DNS 的更多信息。

大多数 Linux 发行版默认都包含 Samba，但某些发行版不包含 AD 客户端实现所需的身份映射服务。如果你从源码编译，这些组件可以被适配以正确设置，因此我们建议安装可用的二进制包。

