
与 xinetd 类似，当你的系统对特定服务的请求很少，且你不需要该服务器一直运行时，就会使用 inetd。只有当远程用户访问其服务时，你才需要它。inetd 是 xinetd 的前身，仍然用于某些发行版和其他 Linux 系统。

inetd 守护进程管理 Internet 服务器，并在当你的系统接收到对这些服务的请求时调用它们。inetd 持续检查远程用户对特定 Internet 服务的任何请求；当它收到请求时，会启动相应的服务守护进程。例如，华盛顿大学 FTP 守护进程 `wu-ftpd` 通常使用 inetd 安装，而不是作为独立的守护进程。当 inetd 收到用户访问 FTP 的请求时，它会启动 `in.ftpd`（FTP 守护进程），然后处理请求，允许远程用户下载文件。

为了让 inetd 调用适当的守护进程，必须在 `/etc/services` 和 `/etc/inetd.conf` 文件中进行配置。`/etc/services` 列出了系统上可用的服务。`/etc/services` 中的条目由服务名称以及其端口和协议组成，并用斜杠分隔。这里显示了在你的 `/etc/services` 文件中显示的 FTP 条目。其他发行版可能对 FTP 只有一个条目。

`/etc/inetd.conf` 文件是 inetd 的配置文件。对于其条目，你指定服务、其协议和服务器程序。这里显示了 FTP 条目。服务器路径和参数可能根据不同的 Linux 发行版而异。某些程序有一个特殊的脚本、链接或替代程序用于 inetd 激活，而不是直接使用程序。

| 服务 | 协议 | 服务器程序 |
| :--- | :--- | :--- |
| FTP | tcp | /usr/sbin/in.ftpd |

（省略重复内容）

## TCP Wrappers

TCP wrappers 为 `hosts.allow` 和 `hosts.deny` 文件增加了另一层安全保护。以下表列出了可用的通配符：

| 通配符 | 描述 |
| :--- | :--- |
| ALL | 匹配所有主机。 |
| LOCAL | 匹配仅指定主机名的主机。 |
| UNKNOWN | 匹配地址未知的主机。 |
| KNOWN | 匹配已知的主机。 |
| PARANOID | 匹配主机名与其 IP 地址不匹配的主机。 |
| EXCEPT | 一个允许你对匹配进行排除的运算符。其形式为 list1 EXCEPT list2，其中匹配 list1 且匹配 list2 的项将被排除。 |

在 Red Hat 的 `inetd.conf` 文件中，ftpd 服务器条目已经配置完成。这里不是 ftpd 程序 `/usr/sbin/in.ftpd` 的路径，而是 tcpd 守护进程的路径 `/usr/sbin/tcpd`。随后的参数字段列出了 in.ftpd 服务器程序。

```
# <service> <sock_type> <proto> <flags> <user> <server_path> <args>

ftp stream tcp nowait root /usr/sbin/tcpd in.ftpd
```

当 `inetd` 接收到 FTP 服务请求时，它会调用 tcpd 守护进程，然后由该进程接管并监控连接。它会启动 in.ftpd 服务器程序。默认情况下，tcpd 允许所有请求。若要专门针对 FTP 服务允许所有请求，你需要在 `/etc/hosts.allow` 文件中输入以下内容。`ALL:ALL` 条目允许所有主机通过所有服务访问你的系统。

```
ftp:ALL
```

`/etc/initd.conf` 文件中列出的标准 Internet 服务都使用 tcpd 守护进程，如下所示：

```
# These are standard services.

#nftftp stream tcp nowait root /usr/sbin/tcpd in.ftpd -l -a

telnet stream tcp nowait root /usr/sbin/tcpd in.telnetd
```

# Linux 完全参考

# 第 20 章

## FTP 服务器

Linux：完全参考

文件传输协议（FTP）旨在跨网络从一个系统传输大文件到另一个。与 Internet 操作一样，FTP 基于客户端/服务器模型工作。FTP 客户端程序使用户能够向运行 FTP 服务器程序的远程系统传输文件。第 14 章讨论了 FTP 客户端。任何 Linux 系统都可以作为 FTP 服务器运行。它只需要运行服务器——一个具有适当配置的 FTP 守护进程。传输在客户端和服务器系统的账户之间进行。远程系统上的用户必须登录服务器上的某个账户，然后只能在该账户的目录中传输文件。一种名为 `ftp` 的特殊用户账户允许任何用户使用“anonymous”作为用户名登录。该账户拥有一套被认为是公共的目录和文件，网络上任何想要下载它们的人都可以访问。互联网上大量的 FTP 站点都是支持匿名登录 FTP 账户的 FTP 服务器。任何 Linux 系统都可以配置为支持匿名 FTP 访问，成为网络 FTP 站点。此类站点可以在内域网或互联网上运行。

> 在 Mandrake 和 Red Hat 上，匿名 FTP 的配置文件位于以 `antftp` 开头的包中。安装此包将设置你的 FTP 目录并配置 FTP 账户。

# FTP 守护进程

FTP 服务器由一个 FTP 守护进程和配置文件组成。守护进程是一个持续检查来自远程用户 FTP 请求的程序。当收到请求时，它会管理登录、建立与请求用户的连接，并执行用户发送的任何 FTP 命令。对于匿名 FTP 访问，FTP 守护进程允许远程用户使用 `anonymous` 或 `ftp` 作为服务器登录 FTP 账户。然后用户就可以访问为 FTP 账户设置的目录和文件。作为进一步的安全措施，守护进程会将该会话的根目录更改为 FTP 目录。这向远程用户隐藏了系统。通常情况下，系统上的用户可以移动到任何向其开放的目录。使用匿名 FTP 登录的用户只能看到 FTP 目录及其子目录。系统的其余部分对该用户是不可见的。这种效果通过 `chmod` 操作（后文将讨论）实现，该操作字面上为该 FTP 用户更改了系统根目录。默认情况下，FTP 服务器还要求用户使用有效的 shell。它会检查 `/etc/shells` 文件中的 shell 列表。大多数服务器守护进程都有关闭此功能的选项。

Linux 系统上有多个 FTP 服务器守护进程可用。大多数 Linux 发行版都带有来自华盛顿大学的 FTP 服务器 `wu-ftpd`。你可以从它们的 FTP 站点（如 ftp.redhat.com）下载特定发行版的 RPM 更新包。该软件包通常以 `wu-ftpd` 为头。

# 第 20 章：FTP 服务器

从华盛顿大学归档库获取原始压缩包：http://wuarchive.wust.edu/packages/wuarchive-ftpd（此处链接为示例）

ProFTPD 是一种基于 Apache Web 服务器设计的更新且流行的 FTP 守护进程。它的特点是配置简化并支持虚拟主机。虽然目前未包含在大多数发行版中，但你可以从发行版站点以及 ProFTPD 网站下载 RPM 包。该包名称以 `ftpd` 为头。最新版本的压缩包以及文档可以在 ProFTPD 网站 www.proftp.net 获取。另一个 FTP 守护进程 `ncftpd` 免费供学术使用，并对小型网络收取较低费用。请访问 www.ncftpd.org 了解更多信息。

还有几种基于安全的 FTP 服务器可用，包括 SSLftp 和 SSH sftp。SSLftp 使用 SSL（安全套接层）对传输进行加密和身份验证，并使用 MD5 摘要检查传输文件的完整性。SSH sftp 是现在 Open SSH 软件包的一部分的 FTP 服务器，使用 SSH 加密和身份验证建立安全的 FTP 连接。

包括 Red Hat、Mandrake 和 Caldera 在内的大多数发行版目前在安装期间都会安装 `wu-ftpd` 服务器和 anon FTP 包。此时，会创建一个带有若干子目录的 anon FTP 目录，你可以在其中放置供 FTP 访问的文件。在 Mandrake 和 Red Hat 上，匿名 FTP 的配置文件位于以 `antftp` 开头的包中。安装此包将设置你的 FTP 目录并配置 FTP 账户。

# Linux：完全参考

> FTP 账户的普通用户可以获得其账户权限。

# 匿名 FTP：anon

匿名 FTP 站点本质上是你系统上的一个特殊用户，其主目录是公开可访问的。任何人都可以登录此账户并访问其文件。因为任何人都可以登录匿名账户，所以你必须小心限制远程 FTP 用户访问系统的任何部分。

# FTP 用户账户：anonymous

为了允许其他用户通过匿名 FTP 访问你的系统，你必须拥有一个名为 `FTP` 的用户账户。大多数发行版已经为你创建了该账户。如果你的系统没有此类账户，你将不得不创建一个。

## 第 20 章：FTP 服务器

该文件防止普通用户访问。以下是你在 Mandrake 和 Red Hat 系统的 `/etc/passwd` 文件中可以找到的条目，它设置了作为匿名用户进行 FTP 登录：

```
ftp::*:14:50:FTP User:/var/ftp:
```

密码字段中的星号 `*` 锁定了该账户，防止其他用户访问它，从而获得对其文件的控制权或访问你系统的其他部分。用户 ID 14 是一个唯一 ID。注释字段为 FTP User。登录目录为 `/var/ftp`。当 FTP 登录你的系统时，它们将被放置在该目录中。如果没有设置主目录，请创建一个并使用 `chown` 命令将其所有者更改为 FTP 用户。

组 ID 是 ftp 组的 ID，该组仅为匿名用户设置。你可以对 ftp 组设置限制，从而限制任何 FTP 用户。这里是你在 `/etc/group` 文件中可以找到的 ftp 组条目。如果你的系统内核没有该条目，你应该手动添加它。

```
ftp::50:
```

### 匿名 FTP 服务器目录

如前所述，在 Red Hat 上，FTP 主目录名为 `ftp` 并放置在 `/var` 目录下。当用户匿名登录时，他们会被放置在此目录中。保护系统的重要部分是防止远程用户使用受限目录之外的任何命令或程序。例如，你不会让用户使用 `ls` 命令列出文件名，因为 `ls` 位于你的 `/bin` 目录。同时，你又想让 FTP 用户使用 `ls` 命令列出文件名。新的 FTP 守护进程（如 ProFTPD）通过创建对所需系统命令和文件的访问权限来解决这个问题，同时将远程用户限制为只能访问 FTP 站点的目录。另一种传统的解决方案（被 weftp 使用）是创建远程用户所需的系统目录和文件的副本，并将它们放置在 `ftp` 目录中，供用户访问。在 `ftp` 目录中放置一个 `bin` 目录，远程用户被限制在该处，而不是系统的 `bin` 目录。每当他们使用 `ls` 命令时，远程用户使用的是 `ftp/bin` 中的那个。

在 Red Hat 上，`anon` 包会设置这些系统目录和文件的副本。否则，你可能需要自己创建这些目录。在 Red Hat 上，`anon` 包会在 `/var/ftp` 目录下安装 `etc`、`bin` 和 `lib` 目录。这些包含了允许 FTP 客户端执行 FTP 命令（如列出或更改配置文件）所需的系统文件的本地版本。`ftp/etc` 目录包含密码和组配置文件的版本，`ftp/bin` 目录包含 shell 和压缩命令的副本，而 `ftp/lib` 目录持有系统库的副本。`anon` 包设置的目录所示：

```
ftp

ftp/bin

ftp/etc

ftp/lib

ftp/pub
```

`ftp/etc` 目录持有专门为 FTP 访问配置的 `passwd` 和 `group` 文件版本。再次，其核心思想是防止 FTP 用户访问 `/etc` 目录中的原始文件。`ftp/etc/passwd` 文件不应包含你系统上任何普通用户的条目。所有条目的密码都应设置为 `*` 以阻止访问。组文件不应包含任何用户组，且所有密码都应被设置为 `*`。

```
ftp/etc/passwd

root*:1:0::

bin*:1:1::

operator*:11:0::

ftp*:14:50::

nobdy*:99:99::

ftp/etc/group

root*:0:

bin::2:

daemon::2:

sys::3:

adm::4:

ftp::50:
```
