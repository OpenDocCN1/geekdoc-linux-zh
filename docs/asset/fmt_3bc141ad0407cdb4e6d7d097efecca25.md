
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

Samba 通常在运行期间不需要太多关注。然而，如果你遇到问题，可以查阅两个主要的调试信息源：每个客户端的日志文件和 `smbstatus` 命令。确保你的配置文件中有恰当的日志设置。

```ini
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

`smbdcontrol` 方便于在不修改 `smb.conf` 的情况下更改运行中的 Samba 服务器上的调试级别。例如：

```
$ sudo smbdcontrol debug "4 auth:10"
```

上述示例将全局调试级别设置为 4，并将认证相关事务的调试级别设置为 10。`smbd` 参数指定系统上所有 smb 守护进程都将设置其调试。要调试特定的已建立连接，你可以使用 `smbstatus` 命令确定哪个 smb 守护进程处理该连接，并将 PID 传递给 `smbd debug` 仅一个连接。在日志级别超过 100 时，你将会在日志中看到（加密的）密码。

`smbstatus` 显示当前活动的连接和锁文件。这些信息在你追踪锁定问题时（例如，“哪个用户打开了文件 xyz 进行独占读/写？”）特别有用。输出的第一部分列出了用户连接的资源。最后部分列出了任何文件锁。

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
