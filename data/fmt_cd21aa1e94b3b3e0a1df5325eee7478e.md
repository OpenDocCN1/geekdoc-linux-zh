
</VirtualHost>

这里 `CustomLog` 指令中的名称 `common` 指的是 `httpd.conf` 文件中由 `LogFormat` 指令更早定义的一个格式的名称，如下所示：

```
LogFormat "%h %l %u %t \"%r\" %>s %b" common
```

此日志格式字符串产生的日志文件中的行如下所示：

```
dial236.dc.psn.net - - [13/Jul/2003:18:09:00 -0500] "GET / HTTP/1.0" 200 1243
```

格式字符串包含以百分号（`%`）开头的两个字母标记。这些标记的含义如表 2-1 所示。

表 2-1 LogFormat 标记

| 标记 | 含义 |
|-------|---------|
| `%b` | 发送到客户端的字节数，不包括头信息 |
| `%h` | 客户端机器的主机名 |
| `%l` | 用户的身份，如果可用 |
| `%r` | 客户端的 HTTP 请求（例如，GET / HTTP/1.0） |
| `%s` | Web 服务器的服务器响应代码 |
| `%t` | 当前本地日期和时间 |
| `%u` | 用户提供的用户名（仅当访问控制规则要求用户名/密码身份验证时） |

# 第三章：设置 FTP 服务器

## 本章内容

- 安装 FTP 服务器
- 配置 FTP 服务器
- 设置匿名 FTP

文件传输协议（FTP）是一种流行的用于在系统之间传输文件的 Internet 服务。匿名 FTP 是另一种用于分发文件的流行 Internet 服务。匿名 FTP 的好处在于，如果远程系统支持匿名 FTP，任何人都可以以匿名用户 ID 使用 FTP 并从该系统下载文件。虽然匿名 FTP 对于分发数据很有用，但如果设置不当会带来安全风险。

Red Hat Linux 附带了多个 FTP 客户端和由 Chris Evans 编写的“非常安全”FTP 守护进程（`vsftpd`）。Red Hat Linux 还包含一个名为 `anonftp` 的 RPM，用于设置支持匿名 FTP 所需的文件。在本章中，我将向您展示如何通过文本配置文件配置 FTP 服务器以及如何控制对 FTP 服务器的访问。我还描述了匿名 FTP——它的设置方式以及如何确保其安全。

### 安装 FTP 服务器

在 Red Hat Linux 安装期间，您可以选择安装 FTP 服务器软件。要检查 FTP 服务器是否已安装，请键入以下命令：

```
rpm -q vsftpd
```

如果软件确实已安装，您应该会看到类似以下内容的输出：

```
vsftpd-1.2.0-2.1
```

以 root 身份登录并将 DVD 放入 DVD 驱动器。如果您使用的是 GNOME 或 KDE 桌面，DVD 应该会自动挂载。如果没有，请键入以下命令来挂载 DVD：

```
mount /mnt/cdrom
```

然后键入以下命令来更改目录：

```
cd /mnt/cdrom/RedHat/RPMS
```

这里可以找到 FTP 的 RPM 文件。您可以使用以下 RPM 命令同时安装 FTP 服务器和匿名 FTP 包：

```
rpm -ivh vsftpd*
```

```
rpm -ivh anonftp*
```

## 配置 FTP 服务器

Red Hat Linux 自带非常安全的 FTP 守护进程（`vsftpd`），由 Chris Evans 编写。`vsftpd` 的可执行文件为 `/usr/sbin/vsftpd`，它使用 `/etc` 和 `/etc/vsftpd` 目录中的多个配置文件。默认情况下，`vsftpd` 服务器处于禁用状态；如果您想使用 FTP 服务器，首先必须启用它。本节将向您展示如何操作。

在 Red Hat Linux 的早期版本中，`vsftpd` 服务器被设置为在 `xinetd` — 互联网超级服务器 下运行。这需要编辑 `/etc/xinetd.d` 目录中的配置文件以启用 `vsftpd` 服务器。然而，从 Red Hat Linux 8.1 开始，`vsftpd` 服务器被配置为独立运行，并且有一个初始化脚本（或 init 脚本）— `/etc/init.d/vsftpd` — 用于启动和停止服务器。要启动 `vsftpd` 服务器，请以 root 身份登录并键入以下命令：

```
service vsftpd start
```

您也可以以 root 身份键入以下命令，使 `vsftpd` 在系统启动时自动启动：

```
chkconfig --level 35 vsftpd on
```
