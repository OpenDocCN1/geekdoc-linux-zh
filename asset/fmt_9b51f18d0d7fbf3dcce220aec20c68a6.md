
```
CustomLog /home/naba/httpd/logs/access_log common

</VirtualHost>
```

这里 `CustomLog` 指令中的名称 `common` 指的是 `httpd.conf` 文件中通过 `LogFormat` 指令定义的格式名称，如下：

```
LogFormat "%h %l %u \"r\ %>s %b" common
```

该日志格式字符串生成的日志文件行看起来所示：

```
dial123.dc.psn.net - [13/Jul/2003:18:09:00 -0500] "GET / HTTP/1.0" 200 1243
```

该格式字符串包含两个以百分号（`%`）开头的两个字母令牌。这些令牌的含义见表 2-1。

| 表格 2-1 | 令牌 | 含义 |
| --- | --- | --- |
| `%b` | 发送到客户端的字节数，不包含头部信息 |
| `%h` | 客户端机器的主机名 |
| `%l` | 用户身份标识，如果可用 |
| `%r` | 来自客户端的 HTTP 请求（例如，GET / HTTP/1.0） |
| `%s` | 来自 Web 服务器的响应代码 |
| `%t` | 当前日期和时间 |
| `%u` | 用户提供的用户名（仅当访问控制规则需要用户名/密码认证时） |

## 第 3 章：设置 FTP 服务器

## 本章内容

- 安装 FTP 服务器
- 配置 FTP 服务器
- 设置匿名 FTP

文件传输协议（FTP）是一种用于从一个系统传输文件到另一个系统的流行互联网服务。匿名 FTP 是另一种用于发布文件的流行互联网服务。匿名 FTP 的优点在于，如果远程系统支持匿名 FTP，任何人都可以使用匿名用户 ID 通过 FTP 从该系统下载文件。虽然匿名 FTP 对于分发数据很有用，但如果设置不当，它会带来安全风险。

Red Linux 带有有几个 FTP 客户端以及由 Chris Evans 编写的“非常安全”的 FTP 守护进程（`vsftpd`）。Red Linux 还包含一个名为 `anonymousftp` 的 RPM 包，用于设置匿名 FTP 所需的文件。在本章中，我将向你展示如何通过文本配置文件配置 FTP 服务器，以及如何控制对 FTP 服务器的访问。我还描述了匿名 FTP——如何设置它以及如何确保它的安全。

## 安装 FTP 服务器

在 Red Hat 安装期间，你可以选择安装 FTP 服务器软件。要检查是否已安装 FTP 服务器，请使用以下命令：

```
rpm -q vsftpd
```

如果软件确实已，你应该看到类似下面的输出：

```
vsftpd-1.2.0-2.1
```

如果你收到提示包未安装的消息，可以轻松地从配套 DVD 安装。要安装 FTP 的 RPM 文件，请以 root 身份登录并插入 DVD。如果你使用 GNOME 或 KDE，DVD 应该会自动挂载。如果没有，输入以下命令进行挂载：

```
mount /cdrom
```

然后输入以下内容进行切换：

```
cd /cdrom
```

要找到 FTP 的 RPM 包，输入以下内容：

```
ls RedHat/
```

要安装 FTP 服务器，使用以下命令：

```
rpm -ivh RedHat/*
```

要检查是否安装了 FTP 服务器，输入：

```
rpm -q vsftpd
```

## 634 配置 FTP 服务器

Red Linux 带有几个 FTP 客户端以及由 Chris Evans 编写的“非常安全”的 FTP 守护进程（`vsftpd`）。Red Linux 还包含一个名为 `anonymousftp` 的 RPM，用于设置匿名 FTP 所需的文件。在本章中，我向你展示如何通过文本配置文件配置 FTP 服务器，以及如何控制对 FTP 服务器的访问。我还描述了匿名 FTP——如何设置它以及如何确保它的安全。

在 Red Hat 8 中，`vsftpd` 服务器被配置在 `xinetd` 下运行。要启动 `vsftpd`，以 root 身份登录并输入：

```
service vsftpd start
```

要停止 `vsftpd`，输入：

```
service vsftpd stop
```

要重启 `vsftpd`，输入：

```
service vsftpd restart
```

要让 `vsftpd` 在启动时自动运行，输入：

```
chkconfig --level 3 vsftpd on
```
