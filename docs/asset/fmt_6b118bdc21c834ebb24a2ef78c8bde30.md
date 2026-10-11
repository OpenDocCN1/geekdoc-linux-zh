
kern* `/var/log/logfile`

```
```

或者，你可以指定多个设施和优先级；要记录除内核警告以外的所有设施错误消息到 `/var/log/logfile`，可以使用以下条目：

```
kern.*=warn /var/log/logfile
```

要记录来自内核和 news 守护进程的所有错误消息到 `/var/log/logfile`，可以使用以下条目：

```
kern,news.* /var/log/logfile
```

要记录除内核以外，所有设施的警告消息，可以使用 `none` 关键字，如下所示：

```
*=none /var/log/logfile
```

表 11-4 描述了日志守护进程使用的不同设施。

| 设施 | 描述 |
| --- | --- |
| authlog | 指定来自登录系统的消息，如 login 程序、 getty 程序和命令 |
| security | 指定跨网络或系统验证用户时的消息 |
| cron | 指定来自 cron 守护进程的消息 |
| daemon | 指定来自系统 守护进程的消息 |
| kern | 指定 Linux 内核的消息 |
| lpr | 指定打印系统的消息 (lpd) |
| mail | 指定邮件系统的消息 (sendmail) |
| mark | 指定时间戳；仅内部使用 |
| news | 指定来自 News 守护进程的消息 |
| syslog | 指定来自 syslog 守护进程的消息 |
| user | 指定来自用户进程的消息 |
| uucp | 指定来自 uucp（UNIX 到 UNIX）的消息 |

表 11-4 日志守护进程使用的设施（继续）

| 设施 | 描述 |
| --- | --- |
| local0-7 | 指定本地消息；这些默认不使用，但可以自定义自定义 |

表 11-5 显示了按升顺序列出的可用优先级。

| 优先级 | 描述 |
| --- | --- |
| debug | 表示特定设施的所有信息 |
| info | 表示系统操作的正常信息消息 |
| notice | 表示应记录以后参考的信息，但尚未指示问题 |
| warning | 表示可能是错误的结果，但对系统操作至关重要 |
| error 或 err | 表示其他优先级未描述的所有错误消息 |
| crit | 表示系统严重错误，例如硬盘故障 |
| alert | 表示应立即纠正的错误，例如数据库损坏 |
| emerg | 表示通常向所有用户广播的严重系统状况 |
| panic | |

## 管理日志文件

虽然日志文件包含重要的系统信息，但随着时间的推移，它们可能会在文件中占用不必要的空间。因此，定期清理日志文件是非常重要的。

不要删除日志文件，因为权限和所有权也会被移除。

在清理日志文件之前，良好的做法是打印它们并将它们存储在安全的地方以便以后参考。要清理日志文件，记住你可以使用 `>` 重定向符号。以下命令显示了 `/var/log/messages` 日志文件在打印前后的大小：

```
[root@server1 ~] ls -l /var/log/messages

-rw------ 1 root root 21705 Jul 14 10:52 /var/log/messages
```

```
[root@server1]# # cp -d printer1 /var/log/messages

[root@server1]# # /var/log/messages

[root@server1]# # ls -l /var/log/messages

-rw------- 1 root 0 Jul 14 10:52 /var/log/messages

[root@server1]# #
```

你还可以使用 `cron` 守护进程定期地打印和清理日志文件。

或者，你可以调度 `logrotate` 工具备份并清理存储在 `/etc/logrotate.conf` 文件中的条目以及存储在 `/etc/logrotate.d` 目录中的文件。`logrotate` 命令通常循环重命名日志文件；测试的日志文件在第一个循环中被重命名为 `test.log.1`，并创建一个新的测试文件来接收系统信息。在第二个循环中，`test.log` 被重命名为 `test.log.1`，并创建一个新的日志文件来接受系统信息。

你可以指定 `logrotate` 保留的日志文件数量。如果 `logrotate` 配置为只保留两个旧日志文件副本（例如 `test.log.1` 和 `test.log.2`），那么 `test.log.2` 在下一个循环中会被重命名。

`/etc/logrotate.conf` 文件的示例所示：

```
[root@server1]# cat /etc/logrotate.conf
# 查看 "man logrotate" 详情

# 每周轮转日志文件

weekly

# 保留 4 周的备份

rotate 4

# 在轮转旧文件后创建新的（空）日志文件

create

# 如果你想压缩日志文件，请取消此注释

compress

# 将日志轮转信息放入此目录

include /etc/logrotate.d

# 拥有 wtmp -- 我们将轮转它

/var/log/wtmp {
  monthly
  create
}

# 特定的配置
```

## 日志文件管理

在前面的输出中，`#` 字符表示注释。被存储在 `/etc/logrotate.d` 中的文件被忽略。被存储在 `/etc/logrotate.d` 中的文件，除非有指定。此外，日志文件将每月轮转，并保留 4 个副本。

`/var/log/wtmp` {
  monthly
  create
}

在前面的输出中，`#` 字符表示注释。被存储在 `/etc/logrotate.d` 中的文件被忽略。此外，日志文件将每月轮转，并保留 4 个副本。

`/var/log/wtmp` {
  monthly
  create
}

在前面的输出中，`#` 字符表示注释。被存储在 `/etc/logrotate.d` 中的文件被忽略。此外，日志文件将每月轮转，并保留 4 个副本。

`/var/log/wtmp` {
  monthly
  create
}

# 管理用户和组 491

组标识符 (`GID`) 是用户的主组 ID。每个用户可以是多个组的成员，但这些组中只有一个可以作为主组。用户的主组是该用户创建的任何文件或目录的所有者组。同样，当用户创建一个文件或目录时，该用户就会成为该文件或目录的所有者。`GECOS` 代表对用户的文本描述，通常留为空；此信息最初用于通用电气综合操作系统 (`GECOS`)。最后两个字段代表用户主目录的绝对路径和 shell 路径。

下面显示了一个 `/etc/passwd` 文件的示例：

```
[root]# cat /etc/passwd
root:x:0:0:root:/bin
bin:x:1:1:bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin/nologin
adm:x:3:4:adm:/var/adm/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
sync:x:5:0:sync:/sbin/sync
shutdown:x:6:6
halt:x:7:0:halt:/sbin/halt
mail:x:8:12:mail:/var/spool:/sbin/nologin
news:x:9:13:news:/etc
uucp:x:10:14:uucp:/var/spool/uucp:/sbin/nologin
operator:x:11:0:operator:/root:/sbin/nologin
games:x:12:100:games:/usr/games/sbin/nologin
gopher:x:13:30:gopher:/var/gopher:/sbin/nologin
ftp:x:14:50:FTP:/var/ftp:/sbin/nologin
nnbody:x:99:99:Nobody:/sbin/nologin
rpm:x:37:37::/var/lib/rpm/sbin/sbin
vcsa:x:69:69:vcsa:console:/dev:/sbin/nologin
scd:x:72:28:NSCD:daemon:/sbin/nologin
ssh:x:74:74:Privilege-separated SSH:/var/empty/sshd/
ident:x:98:98:ident:/sbin/nologin
rpc:x:32:32:Portmapper RPC user:/sbin/nologin
rpcuser:x:29:29:RPC Service User:/var/lib/nfs:/sbin/nologin
nfsobdy:x:6534:6534:Anonymous NFS User:/var/lib/nfs:/sbin/nologin
```
