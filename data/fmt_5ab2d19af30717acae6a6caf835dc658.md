
接下来的章节描述了转换条目中的字段。

## 类型 (Types)

你必须使用类型文件告诉服务器转换规则适用于哪些类型的文件。使用 `;` 字符分隔文件类型条目，并为每个类型赋予值 `T_REG`、`T_ASCII` 和 `T_DIR`。

`T_REG` 表示普通文件，`T_ASCII` 表示 ASCII 文件，`T_DIR` 表示目录。一个典型的条目是 `T_REG ; T_ASCII`，它表示一个普通 ASCII 文件。

## 选项 (Options)

`options` 字段告知服务器正在对文件执行什么操作。与类型文件类似，选项也用 `;` 字符分隔。以下是你可以分配给 `options` 字段中项目的有效范围：

### 第 18 章 安全文件传输协议 (FTP) 服务

- `O_COMPRESS` 用于压缩文件
- `O_UNCOMPRESS` 用于解压缩文件
- `O_TAR` 对文件进行 tar 处理

该字段的一个示例是 `O_COMPRESS; O_TAR`，其中文件既被压缩又经过了 TAR 处理。

## 描述 (Description)

`description` 字段允许管理员快速理解规则的作用。该字段没有任何语法限制，尽管它通常是一个单词条目——例如 `TAR`、`TAR+COMPRESS` 或 `UNCOMPRESS`——这足够传达概念了。

## 转换运行的示例

编写复杂的转换条目是最好交给 Linux/UNIX 专家完成的任务，但 `wu-ftppd` 带的示例 `ftpconversions` 文件为 Red Hat 管理员提供了充足的示例。构建你自己的简单转换条目并不困难，让我们让我们检查并解码一个示例：

```
:Z: :/bin/compress -d %s:T_REG|T_ASCII:0_UNCOMPRESS:UNCOMPRESS
```

在此示例中，删除前缀（字段 1）为空，因为此规则不适用于前缀。该规则的第二个字段包含 `.Z` 后缀；因此它处理的是使用 `compress` 工具压缩的文件。该规则未处理附加前缀或后缀，字段 3 和 4 为空。字段 5 是外部命令字段，告诉服务器运行 `compress` 工具来解压 `-d` 参数指定的文件。`-c` 选项指示将 `compress` 工具的输出写入标准输出（standard out），在本文情况下即服务器。`%s` 是规则应用的文件名。字段 6 指定该文件为 ASCII 格式的普通文件。字段 7 是 `options` 字段，告诉服务器该命令会解压缩文件。最后，最后一个字段是注释，让管理员快速解码转换规则的作用，即解压缩文件。

## 示例 (EXAMPLES)

`wu-ftppd` 的默认 `ftpconversions` 文件中可能指定多个转换规则。额外的示例（例如针对 Sun 的 Solaris 系统的示例）可能在额外的 `wu-ftppd` 文档中可用。

## 在 ftphosts 文件中使用命令允许或拒绝 FTP 服务器连接

`ftphosts` 文件的目的是允许或拒绝特定用户或地址连接 FTP 服务器。该文件的格式是单词 `allow` 或 `deny`，可选跟随一个用户名，然后是 IP 地址或 DNS 地址。

```
allow username address

deny username address
```

列表 18.4 显示了该文件的示例配置。

### 列表 18.4 允许或拒绝用户的 ftphosts 配置文件

```
# 示例主机访问文件

#

# '#' 之后的所有内容都被视为注释，

# 空行被忽略
allow tdc 128.0.0.1

allow tdc 192.168.101.*

allow tdc insanepenguin.net

allow tdc *.exodus.net

deny anonymous 201.*

deny anonymous *.net
```

`*` 是一个通配符，可以匹配任何组合。同样，`allow tdc *.exodus.net` 将允许用户 `tdc` 登录服务器。系统配置文件的更改在你重启 `xinetd` 后生效。要重启 `xinetd`，请使用命令 `/etc/rc.d/init.d/xinetd`。

```
# /etc/rc.d/init.d/xinetd
```

```
Stopping xinetd: [ OK ]
Starting xinetd: [ OK ]
```

重启后，FTP 服务器即可对所有请求进行访问。

## 服务器管理 (Server Administration)

Wu-ftp 提供了几个命令来辅助服务器管理。这些命令有：

- `ftpwho`——显示当前用户
- `ftpcount`——按类显示当前用户
- `fpshut`——提供自动关闭和用户通知
- `ftrestart`——提供自动重启和消息删除

这些命令都必须以超级用户权限执行，因为它们引用 `ftpaccess` 文件来获取服务器信息。

### 显示连接用户的信息 (Display Information About Connected Users)

此命令提供当前连接到 FTP 服务器的用户信息。命令行如下：

```
/usr/bin/ftpwho
```

表格 18.3 显示了 `ftpwho` 输出的格式。

#### 18.3 ftpwho 字段

| 名称 | 描述 |
|---|---|
| Process ID | FTP 服务器进程的进程 ID。 |
| TTY | 进程的终端 ID。这将始终为 ?，因为 FTP 守护不是交互式登录。 |
| Status | FTP 进程的状态。值为 S: 睡眠，Z: 僵尸（表示崩溃），R: 运行，N: 正常进程 |
| Time | 进程使用的经过处理器时间（分钟和秒）。 |
| Details | 告知哪个主机正在连接、连接的用户以及正在执行的命令。 |

列表 18.5 显示了该命令的典型输出。它列出了处理请求的 FTP 守护的进程 ID、特定用户所属的类别、连接总时间、用户连接时的用户名以及其会话状态。

你可以向 `ftpwho` 传递一个参数。（你可以通过使用 `ftpwho --help` 命令找到该参数。）你可以传递给 `ftpwho` 的唯一参数是 `-v`。该参数会打印 `wu-ftpd` 的版本和许可信息，如下所示：

```
# ftpwho
Service class all:
10447 ? SN  0:00 ftppd: localhost:anonymous/winky@disney.com: IDLE

1 users (no maximum)
```

使用 `-V` 选项的 `ftpwho` 输出显示版本信息，见列表 18.5。

### 列表 18.5 ftpwho -V 命令输出

Copyright © 1999, 2000, 2001 WU-FTPD Development Group.
所有权利保留。

部分版权所有 © 1980, 1985, 1988, 1990, 1991, 1993, 1994
加州大学摄政会。
部分版权所有 © 1993, 1994 圣路易斯华盛顿大学。
部分版权所有 © 1996, 1988 Berkeley Software Design, Inc.
部分版权所有 © 1989 麻萨诸顿学院。
部分版权所有 © 1998 Sendmail, Inc.
部分版权所有 © 1983, 1995, 1996 Eric P. Allman.
部分版权所有 © 1997 Stan Barber.
部分版权所有 © 1997 Kent Landfield.
部分版权所有 © 1991, 1992, 1993, 1994, 1995, 1997
Free Software Foundation, Inc.

本软件及其源代码的使用和分发受 WU-FTPD 软件许可（"LICENSE"）条款的约束。

如果你没有收到许可副本，可以从网上 http://.wu-ftpd.org/license.html 获取。
版本 wu-2.6.2-8

### 统计连接数

`/usr/bin/ftpcount` 用于统计连接到 FTP 服务器的用户数以及允许的最大用户数。在 `ftpwho` 命令的输出末尾也可以找到相同的信息。该命令仅接受一个参数 `-V`，显示与之前的 `ftpwho` 示例相同的输出。

```
# ftpcount
Service class all             4 users (no maximum)
```

### /usr/sbin/ftshutdown 调度 FTP 服务器停机

与任何服务器管理一样，让 FTP 服务器的用户了解即将发生的停机、服务器何时进行更新以及其他相关的站点信息始终是一项良好的做法。`ftshutdown` 命令允许管理员根据传递给它的某些参数，在特定时间关闭 FTP 服务器。该命令的格式如下，并在 `ftshutdown` 页面中有记录：

```
ftshutdown [-V] [-l min] [-d min] time [ warning-message ... ]
```
