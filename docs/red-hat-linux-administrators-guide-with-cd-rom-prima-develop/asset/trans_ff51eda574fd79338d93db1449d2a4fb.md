

二进制文件可能已经以 RPM 格式编译，或者作为独立的单独二进制文件存在，并且可用的选项，如配置文件和其他附件，已经确定。本章提供的说明将更详细地检查从源代码编译和运行 sendmail 的步骤。要获得真正可管理的 sendmail 配置，其中所有设置均由用户确定，从源代码编译是最佳选择。

首先，您希望从 sendmail 主站点获取最新版本的 sendmail：

```
http://www.sendmail.org/
```

您也可以使用 ftp 从同一域名接收源代码：

```
ftp ftp.sendmail.org
```

由于 sendmail 源代码处于积极开发中，您无法确定哪个发布版本或版本号是最稳定的。与 Linux 可用的其他开发软件不同，sendmail 的开发版本相当可靠。您可以毫无顾虑地下载最近的 sendmail 版本并将其安装到您的机器上。通常，安装 CD 上可用的 RPM 版本能够满足大多数网络或系统对电子邮件传递的需求。否则，对于那些更具冒险精神的管理员——那些将程序定制以完全满足系统需求的人——建议他们获取源代码并从头开始安装。在服务器的任何位置解压和 untar 文件。我倾向于将所有源文件保存在一个位置，以防程序需要重新编译。随着时间的推移，二进制文件可能会损坏，在这种情况下，修复文件的最简单方法是创建一个新的二进制文件或复制之前创建的二进制文件覆盖损坏的文件。我通常在 Linux 服务器上创建 /usr/local/gnu 目录。在这里，我拥有最新开发版本的所有源文件。

解包源代码后，切换到新 sendmail 目录的位置，~/sendmail-8.11.0/src/。重要的是，首先要进入 src/ 目录，并自定义与 sendmail 配置和性能相关的设置。有关完整说明，请阅读 install 或 readme 文件，但对于简化版本，您只需输入 ./Build 或 sh Build 即可运行安装。确保您的 $PATH 正确，以便 make 命令顺利运行。在 Red Hat Linux 发行版中，运行 make 命令应该没有问题。

## 构建配置文件

现在编辑 ~/sendmail-8.11.0/cf/cf/ 目录中的 *.mc 文件。文件名代表 m4 宏文件。此文件决定了您的 sendmail 配置以及 sendmail 运行系统所需的变量。sendmail 程序提供了多个不同的示例 .mc 文件，您可以使用它们来创建自己的配置。大多数都针对其他 UNIX 平台以及特定的 Linux 需求进行了配置，因此请寻找与您自己系统最接近的一个。

generic-linux.mc 文件适用于大多数 Linux 发行版，并将生成 sendmail.cf 文件，即配置文件，sendmail 二进制文件将从中查找处理特定请求的说明。否则，您可以使用提供的 redhat.mc 文件来生成针对 Red Hat 发行版定制的 sendmail.cf 文件。要创建可用的 sendmail.cf 文件，您必须首先编辑随附源码的 generic.mc 文件，或者如果您安装了所有 sendmail 包，则编辑随 Red Hat 发行版提供的 *.mc 文件。然后，您必须将 generic.mc 文件通过预处理器运行，从而创建通用的 sendmail.cf 文件。

在 sendmail-8.11.0/cf/cf/generic-linux.mc 中找到 sendmail.mc 文件。为了方便起见，我将 generic-linux.mc 文件复制为 kerry-linux.mc，以便更容易编辑。这样，如果我犯了无法修复的错误，我总可以获取原始副本进行进一步编辑。在任何情况下，将发行版文件复制为另一个文件名以便根据您的需求进行编辑都是个好主意。

通用的 sendmail.mc 文件通常非常有限。以下是其内容的总和：

```
divert(0)dnl
VERSIONID('$Id: generic-linux.mc,v 8.1 1999/09/24 22:48:05
 gshapiro Exp $')
OSTYPE(linux)dnl
DOMAIN(generic)dnl
MAILER(local)dnl
MAILER(smtp)dnl
```

您应该熟悉这些选项，或者查看提供的其中一个示例 *.mc 文件。为了更好地理解哪些选项可以编译到 sendmail 配置中，让我们首先看看 Red Hat 附带的 sendmail.mc 文件，该文件已经提供了一些选项（参见清单 17.1）。

### 清单 17.1 一个带有若干选项的通用 sendmail.mc 文件，用于生成安全的 sendmail.cf 文件

```text
divert(-1)
include('/usr/lib/sendmail-cf/m4/cf.m4')
define('confDEF_USER_ID', "8:12")
OSTYPE('linux')

undefine(`UUCP_RELAY`)
undefine(`BITNET_RELAY`)
define(`confAUTO_REBUILD`)
define(`confTO_CONNECT', '1m')
define(`confTRY_NULL_MX_LIST',true)
define(`confDONT_PROBE_INTERFACES',true)
define(`PROCMAIL_MAILER_PATH', '/usr/bin/procmail')
FEATURE(`smrsh','/usr/sbin/smrsh')
FEATURE(mailertable)
FEATURE(`virtusertable',`hash -o /etc/mail/virtusertable')
FEATURE(redirct)
FEATURE(always_add_domain)
FEATURE(use_cw_file)
FEATURE(local_procmail)
MAILER(procmail)
MAILER(smtp)

FEATURE(`access_db')
FEATURE(`blacklist_recipients')
FEATURE(`accept_unresolvable_domains')
dnl FEATURE(`relay_based_on_MX')
```

您可以使用清单 17.1 中的配置来定义自定义 *.mc 文件，您可以将其命名为任意名称。虽然此清单中定义的选项可能看起来有些令人困惑，但编辑通用的 *.mc 文件比更改生成的 sendmail.cf 文件中的选项更容易。这些功能中的许多都隐藏在 sendmail 配置文件的深层内部。

## 解读 sendmail 规范

为了让您更好地理解每一行实现了什么，本节依次查看 `.mc` 文件中的每一行，并解释它们在 sendmail 下如何工作。您可以在 sendmail 文档中找到更具体的用法。

```
divert(-1)
include(`/usr/lib/sendmail-cf/m4/cf.m4')
```

第一行告诉 m4 预处理器实际配置文件开始的位置。第二行包含该文件，该文件定义了您解析 generic-linux.mc 文件为人类可读格式或标准 sendmail.cf 文件所需的宏。

```
define(`confDEF_USER_ID',`8;12')
```

此行设置了 sendmail 的默认用户和组 ID。数字 8 是运行 sendmail 守护进程的用户 UID，数字 12 是 GID。检查您的 /etc/passwd 以对该用户配置进行详细更改。出于安全原因，建议创建一个专门用于 sendmail 守护进程的用户和组，尽管它通常以 root 身份运行。如果您担心以 root 身份运行 sendmail，请创建一个 sendmail 或 postmaster 用户来控制守护进程的使用。

```
OSTYPE(`linux')
```

此选项告诉 m4 预处理器包含 Linux 的一些标准设置。

```
undefine(`UUCP_RELAY')
```

此行定义 sendmail 不接受或中继任何 UUCP 寻址的电子邮件。这只是 sendmail 出现的中继问题中的第一个。过去，许多人滥用了与电子邮件服务器相关的权限。现在，开发人员正在锁定所有服务器，以不允许中继。如果您确实希望服务器中继到其他任何主机，您必须自行定义此设置。

```
undefine(`BITNET_RELAY')
```

### 注意

> 中继电子邮件是指允许来自您的域或子网类外部的客户端使用您的邮件服务器向另一个也位于您的域之外的服务器发送电子邮件或电子邮件块。您的邮件服务器成为中继点。由于未经请求的批量电子邮件分发者的滥用行为，管理员强烈反对电子邮件中继。sendmail 程序默认禁用中继。

同样，此行指定 sendmail 不接受来自 .BITNET 伪域名或由常规 DNS 条目不支持的域名的任何邮件。

```
define(`confAUTO_REBUILD')
```

此行通知 sendmail 程序，如果需要，在更改该特定文件中的任何设置后自动重建 /etc/alias 文件。别名文件包含有关本地电子邮件别名的信息。

```
define(`confTIME_CONNECT', '1m')
```

此选项将初始 connect() 的超时设置为 1 分钟。此选项只能缩短内核的连接超时。使用此值是安全的。

```
define(`confTRY_NULL_MX_LIST',true)
```

如果您的邮件服务器是主机的最佳 MX 或邮件记录，并且该选项设置为 true，它将尝试直接连接到该主机。主机可以在 MX 记录中具有多个邮件服务器，如名称服务器条目下定义。如果主要邮件服务器宕机，sendmail 然后将邮件传输到为该系统在 DNS 记录中定义的下一个邮件服务器。有关名称服务器和 MX 记录的进一步说明，请参阅第 15 章。

```
define(`confDONT_PROBE_INTERFACES',true)
```

如果您将此选项设置为 true，sendmail 不会将任何本地接口添加到已知等效地址列表中。将此选项保留为默认设置应该是安全的。

```
FEATURE(`smrsh', '/usr/bin/smrsh')
```

