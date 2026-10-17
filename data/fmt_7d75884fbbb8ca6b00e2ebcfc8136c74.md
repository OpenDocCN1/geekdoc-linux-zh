
Linux 的 `resolv.conf` 文件指定了该域正确的名称服务器，Solaris 的 `resolv.conf` 文件也是如此。`search` 和 `domain` 行为不完全的主机名提供了后缀——例如使用 `telnet sleep` 而不是 `telnet sleep.um.edu`。

Linux 的 `nsswitch.conf` 中的 `hosts:` 记录指示首先尝试从 `/etc/hosts` 记录解析名称，然后是 NIS，最后是 DNS。相应的 Solaris 记录则说明搜索 `/etc/hosts`，然后是 DNS。

# 初始配置

实际上，如果你是第一次安装这两个任一参考系统，安装过程会专门地向你询问 IP 地址、子网掩码、默认网关、名称服务器等，并作为安装的一部分相应地配置系统。只要你理解了所要求的内容（这实际上正是本章的主题），你就可以提前从网络管理员那里获取这些信息，并在安装期间直接输入即可。

# 重新配置

有时，你需要更改网络配置，而不一定非要通过完整的重新安装。在 Linux 上，一个 GUI 工具可以帮助你完成此操作。输入命令 `control-panel` 来调用它，选择网络图标，然后进行任何必要的更改。更改网络配置后，重启是一个好主意。

此外，Solaris 8 和 RH Linux 7.1 都提供了 `/usr/sbin/sys-unconfig`，它可以移除特定于运行该系统的所有配置数据。它会撤销安装时发生的配置，然后关闭系统。当系统再次启动时，它会识别出自身未经过配置，并使用首次启动和安装时执行的相同配置。由于 `sys-unconfig` 仅限于配置文件，因此实际上非常简单，例如，执行 `sys-unconfig`，让系统关机，移动到具有不同网络的新位置，启动并为新网络进行配置，同时保留用户身份验证信息、主目录和大多数已安装软件。

![](img/cd7b8bd6bc2bb54927442d4cbe51a330_279_0.png)

# 服务与端口

正如你可能已经知道的，Unix 是多用户操作系统。它同时运行许多进程，其中一些由用户启动并控制，另一些则由操作系统本身启动并控制。通常，Unix 系统会运行几个基于网络的进程、客户端和服务器。

我们已经描述了传输如何从一个节点到达互联网。现在，我们需要考虑在到达后对其进行什么处理。传输负载包含电子邮件，它应该发送到 `sendmail` 进程。如果传输是 `telnet` 会话的一部分，它应该进入 `telnet` 服务器。就此而言，如果有两个 `telnet` 会话正在运行，传输必须进入它所属的那一个。在传输到达时尝试分类其性质和妥善处理是一项艰巨的任务，因为这项工作是在准备传输时通过向数据添加更多信息来完成的。

如果传输要进入 `sendmail` 进程，它会被标记。如果它要进入 `telnet` 服务器，它会被标记为 `telnet` 服务器。如果它是 `telnet` 会话的一部分，它会被标记为该特定的会话。这是计算机世界，所以标记是用数字完成的。正如传输有源地址和目的 IP 地址，它也有源地址和目的端口号。

（注：原文此处存在大量重复的“Common Internet services are...” 句子，根据翻译要求已在逻辑上处理或保留语意，为了文档完整性，此处遵循了原文的结构性描述。）

## 基础操作

第一部分

如果没有特定的服务需要通过 `inetd` 暴露，我们建议将其完全禁用以减少安全风险。如果在使用程序时无法移除 `inetd`，我们建议禁用所有未使用的服务。特别是 `charg`、`echo`、`time` 和 `daytime` 服务几乎从未用于合法目的；它们主要用作拒绝服务攻击的一部分，或利用服务本身的安全漏洞。所有这些服务都应该禁用。它们已经被 `ssh` 软件套件取代（有关 `ssh` 的更多详细信息请参阅第 8 章）。`rsh` 和 `rexec` 也也应该被禁用[注：原文为 "rsh, rexec also be disabled"]；如果你有多个用户登录到你的系统，`ident` 服务器可能有助于确定谁访问了特定的远程资源，但它是不可靠的，且通常没有必要。`telnet` 和 `ftp` 都存在安全风险，在无法将特定用户迁移到 `ssh` 的情况下应禁用它们；因为 Windows、Unix 和 Macintosh 都有免费的客户端，启用 FTP 的唯一理由是系统正在运行匿名 FTP 服务器；除非有像 AMANDA 这样的备份软件在使用，否则 `inetd` 通常可以被禁用。

尽管 `inetd` 和 `xinetd` 的功能方式和目的相似，但它们的配置文件语法完全不同。`inetd` 的配置位于 `/etc/inetd.conf` 中，每个服务由配置文件中的单行表示。以 `#` 开头的行是注释，会被忽略。除了 `/etc/services` 文件中找到端口号和端口名称外，每一行后面都跟着几个其他参数，如 `man` 页面中记录的那样。有四个这样的参数，它们用空格分隔，随后是端口打开时要运行的命令。要禁用服务，只需在行开头添加一个 `#` 符号；要启用服务，只需取消该行的注释。任何需要通过 `inetd` 运行的服务都应该记录其配置设置；注意安装说明，这样你就没问题了。

`xinetd` 的配置语法与 `inetd` 没有任何相似之处。该文件为 `/etc/xinetd.conf`，但在从源码编译而非通过系统安装 `xinetd` 的系统中，其位置可能会有所不同。每个服务由一组开头为 `service <servicename>` 的行表示，`<servicename>` 是 `/etc/services` 文件中列出的服务。随后是一个左大括号 `{`，然后是属性和值的列表，这些本质上是配置变量。每行提供一个属性、一个空格、等号以及该属性的值。重要的属性是 `disable`，如果不需要运行服务，应将其设置为 `yes`；如果需要运行服务，则应设置为 `no`。特定服务的属性后紧跟一个带有右大括号 `{}` 的行。`xinetd.conf(5)` `man` 页面上记录了许多额外的属性；这读起来很有趣，我们鼓励构建构建的系统管理员学习如何充分利用 `inetd`。

`inetd` 和 `xinetd` 在启动时或接收到 HUP 信号时重新读取其配置。在编辑了配置文件或多个文件后，务必在相应的进程上运行 `-HUP`。在旧平台上的某些旧版本 `inetd` 上（特别是早于版本 6 的 SGI IRIX），HUP 信号不会导致配置文件的重新读取，需要杀死并重启进程才能使更改生效。

Solaris 8 使用的是纯净的 `inetd` 配置，类似于版本 7 之前的 Red Hat Linux 版本。版本 7 及更高版本使用 `inetd`，并带有一个最小的 `/etc/xinetd.conf`，其中包含一个 `/etc/xinetd.d` 目录，该目录包含多个文件，每个文件对应一个服务。这对于包管理通过添加或删除单个文件来管理服务非常简单；要在不从系统中完全移除的情况下禁用服务，只需将 `disable = no` 选项改为 `disable = yes`。

## netstat

你可以不带参数使用 `netstat` 或使用 `-a` 参数来查找系统连接状态。关于 `netstat` 输出（无论是否带有 `-a` 参数）的完整讨论出了本章的范围。我们只需在这里粘贴一些精彩片段。

### 列表 5.9 netstat -a 输出

```
# netstat

Active Internet connections (w/o servers)

Proto Recv-Q Send-Q Local Address       Foreign Address State

tcp 0               corylus.ucs:ssh         umbc7.um.edu:36899 ESTABLISHED

tcp 0               corylus.ucs:ssh         cko.ucs:21483 ESTABLISHED

# netstat -a

Active Internet connections (servers and established)

Proto Recv-Q Send-Q Local Address       Foreign Address State

tcp 0               *:32768                *:       LISTEN

tcp 0               *:sunrpc               *:       LISTEN

tcp 0               *:v1                   *:       LISTEN

tcp 0               *:ssh                  *:       LISTEN

tcp 0               localhost.lacdom:smtp  *:       LISTEN

tcp 0               corylus.ucs:ssh         umbc7.um.edu:36899 ESTABLISHED

tcp 0               corylus.ucs:ssh         cko.ucs:21483 ESTABLISHED
```
