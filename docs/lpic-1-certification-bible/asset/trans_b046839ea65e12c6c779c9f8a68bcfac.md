
| 其他功能 | 函数 |
| --- | --- |
| `shutdown <path>` | 服务器会定期检查 <path> 中指定的文件，以确定服务器是否即将关闭。该文件具有以下格式：<year><month><day> <hour><minute><second><deny_offset> <time_zone> <disc_offset> <text>。<deny_offset> 和 <disc_offset> 指定在关闭前拒绝连接并断开连接的时间偏移量。 |
| `daemonaddress <address>` | 定义服务器将监听 IP 地址。默认为所有地址。 |
| `virtual <address><root|banner|logfile><path>` | 启用虚拟服务器功能。 |

| 权限功能 | 函数 |
| --- | --- |
| `chmod <yes|no> <typelist>` | 设置更改文件权限的能力。 |
| `delete <yes|no> <typelist>` | 设置删除文件的能力。 |
| `overwrite <yes|no><typelist>` | 设置覆盖文件的能力。 |
| `rename <yes|no> <typelist>` | 设置重命名文件的能力。 |
| `umask <yes|no> <typelist>` | 设置文件创建权限的能力。 |
| `passwd-check<none|trivial|rfc822>(<enforce|warn>)` | 设置服务器为匿名 FTP 执行的密码检查级别。可用选项如下：<br><br>`none` – 不执行密码检查。<br><br>`trivial` – 密码必须包含 `@` 字符。<br><br>`rfc822` – 密码必须是符合 rfc822 标准的地址。<br><br>以下两个参数设置检查失败时的行为：<br><br>`warn` – 警告用户，并允许用户登录。<br><br>`enforce` – 警告用户，然后注销用户。 |
| `path-filter <typelist><mess><allowed_charset>(<disallowed regexp>...)` | 定义限制文件名或路径中可使用字符的正则表达式。 |

| 权限功能 | 函数 |
| :--- | :--- |
| `upload` `[absolute|relative]` `[class=<classname>]... [-]` `<root-dir>` `<dirglob>` `<yes|no>` `<owner>` `<group>` `<mode>` ["*dirs"|"nodirs"]` `[<d_mode>]` | 通过使用 `<dirglob>` 指定哪些目录可以接收上传。absolute 和 relative 选项指定它是绝对路径名还是相对于当前目录的相对路径名。如果目录设置为允许上传 `<yes|no>`，那么它们将属于 `<owner>` 和 `<group>`，权限为 `<mode>`。 |

## ftphosts 文件

`/etc/ftphosts` 文件用于允许或拒绝其他系统访问您的 FTP 服务器。该文件的格式如下：

```
allow <username> <address glob> [<address glob> ...]

or

deny <username> <address glob> [<address glob> ...]
```

`<address glob>` 可以定义为 CIDR（无类别域间路由）地址或 `address:netmask`。CIDR 寻址遵循 `<network address>/<bits in subnet mask>` 的格式。例如：

```
10.0.0.0/8
```

`address:netmask` 语法如下：

```
10.0.0.0:255.0.0.0
```

如果使用 `allow` 命令，只有被允许的用户和主机可以登录。其他所有用户均被拒绝。另一方面，如果使用 `deny` 命令，任何用户或主机都可以登录，除了那些明确被拒绝的主机。

## ftpusers 和 ftpgroups 文件

`/etc/ftpusers` 文件列出了不能通过 FTP 访问的账户。标准的 Red Hat `/etc/ftpusers` 包含以下内容：

- root
- bin
- daemon
- adm
- lp
- sync
- shutdown
- halt
- mail
- news
- uucp
- operator
- games
- nobody

如您所见，这些是重要的账户，如 root，或者没有理由使用 FTP 的其他账户。如果您只运行匿名 FTP 服务器，将所有账户（匿名账户除外）放入此文件是一个好主意。

/etc/ftpgroups 文件列出了 FTP 用户可以更改密码的组。通常，如果他们知道密码，这会为他们提供更多对站点的访问权限。为使此功能正常工作，/etc/ftpaccess 文件中的 private 条目必须设置为“yes”。

## ftpconversions 文件

/etc/ftpconversions 文件告诉 FTP 服务器如何处理压缩和归档操作。它列出了文件名更改和要使用的程序。文件中的每一行具有以下格式，表 16-5 列出了这些字段：

```
%s:%s:%s:%s:%s:%s:%s:%s
1 2 3 4 5 6 7 8
```

**表 16-5**
**ftpconversions 字段**

| 字段编号 | 功能 |
| :--- | :--- |
| 1 | 去除前缀（目前不支持） |
| 2 | 去除后缀：从文件名中移除指定的扩展名。 |
| 3 | 添加前缀（目前不支持） |
| 4 | 添加后缀：为文件名添加扩展名。 |
| 5 | 外部命令：用于执行操作的命令。 |
| 6 | 类型：操作支持的文件类型。 |
| 7 | 选项：compress、uncompress 和 tar 的选项。 |
| 8 | 描述：描述操作执行的内容。 |

以下是 /etc/ftpconversions 文件的一个示例：

```
.Z: : /bin/compress -d -c %s:T_REG|T_ASCII:0:UNCOMPRESS:UNCOMPRESS
:.Z: .:/bin/compress -c %s:T_REG:0:COMPRESS:COMPRESS
:.gz: .:/bin/gzip -cd %s:T_REG|T_ASCII:0:UNCOMPRESS:GUNZIP
:.gz:/bin/gzip -9 -c %s:T_REG:0:COMPRESS:GZIP
:.tar:/bin/tar -c -f - %s:T_REG|T_DIR:0:tar:TAR
:.tar.Z:/bin/tar -c -Z -f - %s:T_REG|T_DIR:0:COMPRESS|0_TAR:tar+compress
:.tar.gz:/bin/tar -c -Z -f - %s:T_REG|T_DIR:0:COMPRESS|0_TAR:tar+gzip
```

例如，第一个条目启用了解压缩功能，使用 compress -d -c。移除 .Z 扩展名，且不添加其他扩展名。

## FTP 日志文件

/var/log/xferlog 文件（有时在 /var/adm 中找到）显示了到 FTP 服务器和从 FTP 服务器的文件传输。表 16-6 列出了组成日志条目的字段。此日志的语法如下：

current-time transfer-time remote-host file-size filename transfer-type special-action-flag direction access-mode username service-name authentication-method authenticated-user-id completion-status

以下是一个示例 xferlog 文件：

```
Thu Dec 7 20:07:04 2000 1 10.254.90.154 119795 /home/ftp/pub/dhcp-2.0-5.i386.rpm b - o ajason@the-nashes.net ftp 0 * c
Thu Dec 7 20:07:14 2000 1 10.254.90.154 34052 /home/ftp/pub/e2fsprogs-1.18-5.i386.rpm b - o ajason@the-nashes.net ftp 0 * c
Thu Dec 7 20:07:14 2000 1 10.254.90.154 89800 /home/ftp/pub/e2fsprogs-devel-1.18-5.i386.rpm b - o ajason@the-nashes.net ftp 0 * c
```

| 字段 | 信息 |
| :--- | :--- |
| **current-time** | 当前时间，格式为 `"DDD MMM dd hh:mm:ss YYYY"` |
| **transfer-time** | 传输完成所需的秒数 |
| **remote-host** | 远程主机名 |
| **file-size** | 传输的文件大小 |
| **filename** | 文件名 |
| **transfer-type** | 传输类型：a 表示 ASCII；b 表示二进制 |
| **special-action-flag** | 指示何时采取特殊操作的字符：C 表示文件已压缩；U 表示文件已解压；T 表示文件已 tar 压缩；- 表示未采取操作。 |
| **direction** | 传输方向：o 表示传出传输；i 表示传入传输。 |
| **access-mode** | 用户登录的方式：a 表示匿名登录；g 表示来宾账户；r 表示真实用户 |
| **username** | 本地用户名。 |
| **service-name** | 调用的服务名称，通常是 ftp。 |
| **authentication-method** | 认证方法：0 表示无认证；1 表示 RFC931 认证。 |
| **authenticated-user-id** | 从认证方法返回的用户 ID。如果用户 ID 不可用，则使用 *。 |
| **completion-status** | 指定传输是否完成的字符：c 表示传输完成；i 表示传输未完成。 |

## 使用 FTP 服务器工具

您可以使用几种工具来管理 FTP 服务器并监控其功能。这些工具如下：

- ftpshut
- ftpwho
- ftpcount

## ftpshut 命令

`ftpshut` 命令用于在指定时间优雅地关闭 FTP 服务器，同时向用户提供警告。格式如下，表 16-7 显示了参数：

```
ftpshut  [  -V  ] [ -l min] [ -d min] time [ warning-message... ]
```

