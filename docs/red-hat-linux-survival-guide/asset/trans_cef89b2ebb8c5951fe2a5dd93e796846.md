
如果您对前面的命令没有任何输出，则目前尚未安装 wu-ftpd 服务器，需要按照以下各节所述继续进行安装。另一方面，如果您看到已安装的 wu-ftpd 版本，则可以跳过安装部分，直接进入“配置 FTP 服务”部分。

## 安装 wu-ftpd 服务器

关于安装 wu-ftpd 服务器，您有两个选择：安装预编译的 wu-ftpd RPM 包版本，或从 URL ftp://ftp.academ.com/pub/wu-ftpd/private/ 获取源代码并自行编译。由于 Red Hat 提供的 wu-ftpd RPM 包对大多数人来说相当适用，我不描述第二个需要自行编译的过程。

> 我强烈建议您使用 wu-ftpd RPM 包，除非您有非常特殊的原因需要从源代码编译并安装。在后一种情况下，请务必仔细阅读随附的文档。

### 从您的 Red Hat CD-ROM 安装

要从您的 Red Hat CD-ROM 安装 wu-ftpd，请按照以下步骤操作：

- 1. 以 root 身份挂载您的 Red Hat CD-ROM 并将目录更改为 RedHat/RPMS。
- 2. 运行以下命令以定位 wu-ftpd 服务器的 RPM 包：
- 3. 定位到 wu-ftpd 的 RPM 包文件名后，您可以运行以下命令来安装该包：

```
ls | grep wu-ftpd
```

```
rpm -ivh name of the wu-ftpd package
```

例如，以下命令为 Intel 80x86 计算机安装 wu-ftpd 的 2.6.1-16 版本（您的版本号和系统架构可能有所不同）：

```
rpm -ivh wu-ftpd-2.6.1-16.i386.rpm
```

### 从 Red Hat FTP 服务器安装

如果您没有 Red Hat CD-ROM 或想通过 Internet 安装最新版本，您可以运行以下命令：

```
rpm -ivh URL
```

例如，要从名为 ftp://ftp.cdrom.com/ 的匿名 FTP 服务器安装 wu-ftpd-version.i386.rpm 包，该服务器镜像了 Red Hat 发行版，我运行以下命令：

```
rpm -ivh ftp://ftp.cdrom.com/pub/linux/redhat/redhat-7.1/i386/RedHat/RPMS/wu-ftpd-version.i386.rpm
```

如果您想从此类服务器安装，请务必先通过 Web 浏览器浏览该站点以确定正确的 URL。URL 会因您的系统架构（i386、Alpha、Sparc 或其他）以及 Red Hat Linux 和 wu-ftpd 软件的版本而有所不同。

还请注意，如果您尝试在保留旧版本的同时安装更新版本的 wu-ftpd，则必须在 rpm 命令行中提供 --force 选项。

## 配置 FTP 服务

在您安装了 wu-ftpd 或确认其作为 Red Hat 安装的一部分已安装后，您就可以配置新的 FTP 服务器了。您的 FTP 服务器配置由以下文件组成：

- /etc/services
- /etc/xinetd.d/wu-ftpd
- /etc/ftpaccess
- /etc/ftpconversions
- /etc/ftpgroups
- /etc/ftphosts
- /etc/ftpusers

wu-ftpd 服务器像许多其他基于 TCP/IP 的服务器一样，通过名为 xinetd 的 Internet 超级服务器运行，后者侦听端口 21 上的 FTP 连接。当检测到此类连接请求时，它会启动 wu-ftpd 服务器。启动时，xinetd 会查看两个文件以确定哪个服务（端口）与服务器关联。这两个文件是 /etc/services 和 /etc/xinetd.d/wu-ftpd。

### /etc/services

如您可能已知的，/etc/services 文件描述了 Linux 服务器上可用的 TCP/IP 服务。以下行对 FTP 服务器配置很重要：

```
ftp-data      20/tcp
ftp           21/tcp
```

这两行分别告诉 xinetd 为 FTP 服务的数据和命令功能使用哪些端口。默认端口声明是标准的，不应更改。

![](img/9eb7e89292d2f85707b4d49102c865b7_423_0.png)

> FTP 规范（RFC 765）规定 FTP 数据端口（20）比命令端口（21）小一。数据端口值实际上并非源自 /etc/services 中的声明。然而，在 /etc/services 文件中包含数据端口声明可以防止其被意外用于其他用途。

前面的行告诉 xinetd 哪些端口属于 FTP 服务，但它仍需要知道哪个服务器软件负责该服务。这是在 /etc/xinetd.d 目录中保存的文件中定义的。FTP 服务在 /etc/xinetd.d/wu-ftpd 文件中定义。

### /etc/xinetd.d/wu-ftpd

该文件的默认版本如下所示：

```
# default: on
# description: The wu-ftpd FTP server
# serves FTP connections.
# It uses normal, unencrypted usernames and passwords
# for authentication.
```

```
service ftp
{
    socket_type      = stream
    wait             = no
    user             = root
    server           = /usr/sbin/in.ftpd
    server_args      = -l -a
    log_on_success   += DURATION USERID
    log_on_failure   += USERID
    nice             = 10
    disable          = yes
}
```

在这里，service ftp 与名为 in.ftpd 的服务器软件绑定，后者是 wu-ftpd 可执行文件的名称。

-l 和 -a 服务器参数默认指定。-l 选项指定每个 FTP 会话通过 syslog 设施进行记录，而 -a 选项指定在 /etc/ftpaccess 中指定的访问控制配置被启用。这两个参数非常有用，不应删除。要启用 FTP 服务，您必须在此文件中将 disable = yes 改为 disable = no。有关其他选项，请参阅 ftpd 手册页。

![](img/9eb7e89292d2f85707b4d49102c865b7_424_0.png)

如果您对 /etc/xinetd.d/wu-ftpd 或 /etc/services 进行了任何更改，请确保通过发送 SIGUSR1 信号按如下方式通知 xinetd 重新加载配置：

```
kill -USR1 PID_of_xinetd
```

or

```
killall -USR1 xinetd
```

### /etc/ftpaccess

该文件是 FTP 服务器的主要配置文件，并以以下格式包含配置信息：

```
keyword  one_or_more_options
```

默认的 /etc/ftpaccess 文件在列表 14-1 中显示。

#### 列表 14-1 默认的 /etc/ftpaccess 文件

```
class all real,guest,anonymous *

email root@localhost

loginfails 5

readme README* login
readme README* cwd=*

message /welcome.msg login
message .message cwd=*

compress yes all
tar yes all
chmod no guest,anonymous
delete no guest,anonymous
overwrite no guest,anonymous
rename no guest,anonymous

log transfers anonymous,real inbound,outbound

shutdown /etc/shutmsg

passwd-check rfc822 warn
```

该文件是服务器最重要的配置文件，我将在以下各节中对其进行详细讨论。您可以在此文件中指定五种类型的配置信息，即访问配置、信息配置、日志配置、权限配置和杂项配置。这些配置选项将在下面的各节中讨论。

### 访问配置

您可以使用 `class`、`deny`、`limit`、`nor etrieve`、`loginfails`、`private`、`autogroup` 和 `guestgroup` 关键字指定访问配置。

```
class
Syntax: class classname typelist addrglob
Default: class all real,guest,anonymous *
```

`class` 关键字用于定义类名并指定属于该类的用户类型。它还指定类成员可以从中访问 FTP 服务器的 IP 地址或域名。参数如下：

- *类名* 是类的任意名称。
- *类型列表* 是用户类型的以逗号分隔的列表。可用的三种用户类型有：`real`、`anonymous` 和 `guest`。真实用户是指在 `/etc/passwd` 或 `/etc/shadow` 文件中具有有效用户名和密码的人。匿名和访客账户将在本章后面详细讨论。
- *地址通配* 可以是主机的 IP 地址、带通配符的部分 IP 地址（如 `206.171.50.*`）、主机名如 `blackhole.evoknow.com`，或带通配符的部分域名（如 `*.evoknow.com`）。

默认的 `/etc/ftpaccess` 文件包含一个名为 `all` 的类定义，指定类型为 `real`、`guest` 和 `anonymous` 的用户可以从任何地方访问 FTP 服务器。通配符 `*` 用于表示“任何地方”。现在考虑以下示例：

```
class all real 206.171.50.*
```

在这里，仅授予从 206.171.50.0 网络访问服务器的真实用户的 FTP 访问权限。请注意，您也可以使用域名代替 IP 地址。例如：

```
class all real *.evoknow.com *.ad-engine.com
```
