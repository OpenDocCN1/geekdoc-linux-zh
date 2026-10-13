
以下部分描述了转换规则的字段。

## 类型 (Types)

你必须使用 `ftpconversions` 字段告诉服务器适用于哪些文件类型。使用 `|` 字符分隔条目。`T_REG` 表示普通文件，`T_ASCII` 表示 ASCII 文件，`T_DIR` 表示目录。

## 选项 (Options)

选项字段告知服务器对文件执行什么操作。与类型字段类似，选项由 `|` 字符分隔。以下是有效的选项范围：

- `O_COMPRESS` 压缩文件
- `O_UNCOMPRESS` 解压缩
- `O_TAR` 归档文件

该字段的示例为 `O_COMPRESS|O_TAR`，文件经过 TAR 处理。

## 描述 (Description)

描述字段允许管理员快速理解规则的作用。此字段没有语法要求，通常是注释——例如 `TAR,COMPRESS` 或 `UNCOMPRESS`——这足以说明问题。

## 实际转换示例

`wu-ftpd` 的默认 `ftconnections` 文件可能指定多个转换规则。转换规则的更多示例（例如针对 Solaris 操作系统）可以在 `wu-ftpd` 文档中找到。编写复杂的转换规则可能留给专家，但提供的示例已经足够：

```
.z:/bin/compress -c %sO_UNCOMPRESS
```

在这个示例中，剥离前缀（字段 1）为空，因为它尚未实现，所以该规则不适用于前缀。该规则的第二个字段包含 `.z` 后缀；因此它处理使用 `compress` 工具压缩的文件。规则不处理添加前缀或后缀，字段 3 和 4 为空。字段 5 是外部命令，告诉服务器运行 `compress` 工具来解压缩所有扩展名为 `.z` 的文件。`-c` 选项表示将其输出到标准输出，在这种情况下即服务器。`%s` 是规则应用的文件。字段 6 指定该文件是 ASCII 格式的普通文件。字段 7 是选项字段告诉服务器该命令解压缩文件。最后，最后一个字段是注释，让管理员快速解码转换规则的作用；即解压缩文件。

`*` 是一个通配符，可匹配该地址的任意组合。例如，`allow tdc *.exodous.net` 允许用户 `tdc` 从任何包含域名 `exodous.net` 的地址登录 FTP 服务器。同样地，如果匿名用户来自 201 公共 C 类 IP 地址，则不允许其访问 FTP。

对您的系统 `xinetd` 服务器配置文件所做的更改在重启 `xinetd` 后将生效；配置文件仅在启动时进行解析。若要以 root 身份重启 `xinetd`，请执行命令 `/etc/rc.d/init.d/xinetd restart`。这将调用在系统启动和关机时任何运行级别都会调用的同一个 shell 脚本，以启动或停止 `xinetd` 守护进程。`xinetd` 报告其状态如下：

```
# /etc/rc.d/init.d/xinetd restart

Stopping xinetd: [ OK ]

Starting xinetd: [ OK ]
```

当 FTP 服务器重启后，它将对所有入的请求开放。

## 服务器管理

`wu-ftp` 提供了几个命令来辅助服务器管理。这些命令是：

- `ftpwho`—显示当前 FTP 服务器用户的信息
- `ftpcount`—按类别显示当前服务器用户信息
- `ftpshut`—提供自动服务器关机和用户通知
- `ftpstart`—提供自动服务器重启和移除关机消息

这些每个命令都必须以超级用户权限执行，因为它们引用了 `ftppassword` 配置文件来获取 FTP 服务器的信息。

## 显示已连接用户的信息

`ftpwho` 命令提供当前连接到 FTP 服务器的用户信息。其命令行如下：

```
/usr/bin/ftpwho
```

表 24.3 显示了 `ftpwho` 的输出格式。

### 表 24.3 ftpwho 字段

| 名称 | 描述 |
| --- | --- |
| Process ID | FTP 服务器进程的进程 ID。 |
| TTY | 进程的终端 ID。这始终是一个问号 (?)，因为因为 FTP 守护进程不是交互式登录。 |
| Status | FTP 进程的状态。值为：S: Sleeping（休眠），Z: Zombie（僵尸，表示已崩溃） |

### 表 24.3 续

| 名称 | 描述 |
| --- | --- |
| | R: Running（运行），N: Normal process（正常进程） |
| Time | 进程使用的经过处理器的时间，以分钟和秒计。 |
| Details | 说明进程正在连接到谁、来自哪个用户以及当前正在执行的命令。 |

列表 24.5 显示了该命令的典型输出。它列出了处理请求的 ftp 守护进程的进程 ID、该用户所属的类别、总连接时间、用户登录的用户名及其会话状态。

除了关于每个已连接用户的信息外，`ftpwho` 还会显示连接用户的总数，以及 `ftpaccess` 文件中设置的最大数量。此信息可用于监控 FTP 服务器的使用情况。

你可以向 `ftpwho` 传递一个参数。（通过使用 `ftpwho -help` 命令可以找到参数）。你可以传递给 `ftpwho` 的唯一参数是 `-v`。此参数显示了我们的 `wu-ftp` 版本和许可信息，如下所示：

```
# ftppwo

Service class all:

10447 ? SN      0:00 ftppd: localhost:anonymous@winky@disney.com:IDLE

1 users (no maximum)
```

使用 `-V` 选项显示版本信息的 `ftpwho` 输出如列表 24.5 所示。

## 列表 24.5 ftpwho -V 命令输出

Copyright © 1999, 2000, WI-FTPD Development Group.
保留所有权利。

- 部分版权 © 1980, 1985, 1988, 1989, 1990, 1991, 1993, 1994. 加州大学董事会。
- 部分版权 © 1993, 1994 圣路易斯华盛顿大学。
- 部分版权 © 1996, 1998 伯克利软件设计, Inc.
- 部分版权 © 1989 马诸塞理工学院。
- 部分版权 © 1998 Sendmail, Inc.
- 部分版权 © 1983, 1995, 1996, 1997 Eric P. Allman。
- 部分版权 © 1997 Stan Barber。
- 部分版权 © 1991, 1992, 1993, 1994, 1995, 1997 自由软件基金会 Inc.。

## 列表 24.5 续

此软件及其源代码的使用和分发受 WU-FTPD 软件许可（'LICENSE'）条款和条件的约束。

如果你没有收到许可协议的副本，可以在 http://www-ftpd.org/license.html 在线获取。版本 Wu-2.6.2-8。

## 计算连接数

`/usr/bin/ftpcount` 统计连接到 FTP 服务器的用户数以及允许的最大用户数。相同的信息也可以在 `ftpwho` 命令的输出末尾找到。该命令仅接受一个参数 `-V`。

```
/usr/bin/ftpcount

Service class all:

10447 ? SN      0:00 ftppd: localhost:anonymous@winky@disney.com:IDLE

1 users (no maximum)
```
