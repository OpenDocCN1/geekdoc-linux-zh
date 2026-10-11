
### 套接字类型
套接字类型条目告诉系统预期建立何种类型的连接——可靠的双向连接（`stream`）、开销较小的低可靠性连接（`dgram`）、网络底层连接（`raw`）或其他各种类型。这些类型之间的差异在技术层面上非常专业；编辑此条目时，你主要应关注正确输入服务器文档中指定的值。

### 协议
这是使用的 TCP/IP 传输层协议，通常是 `tcp` 或 `udp`。

### 等待/不等待
对于 `dgram` 套接字类型，此条目指定服务器是连接客户端并释放套接字（`nowait`），还是处理完所有数据包后超时（`wait`）。使用其他套接字类型的服务器应在此字段中指定 `nowait`。

### 用户
这是用于运行服务器的用户名。`root` 和 `nobody` 用户是常见的选择，但也可能存在其他选项。作为一般原则，出于安全预防措施，应尽量以低权限用户运行服务器。不过，某些服务器需要 `root` 访问权限。详情请查阅服务器文档。

### 服务器名称
这是服务器的文件名。在前述示例中，服务器指定为 `/usr/sbin/tcpd`，即 TCP Wrappers 二进制文件。该程序提供了一些安全检查，使你可以基于来源等因素限制对服务器的访问。

### 参数
服务器名称之后的所有内容都是传递给服务器的参数。如果你使用 TCP Wrappers，则在此字段中传递真实目标服务器的名称（例如 `/usr/sbin/ftpd`）及其参数。

井号（`#`）是 `/etc/inetd.conf` 中的注释符号。因此，如果某个服务器是通过 `inetd` 运行的且你想禁用它，可以在该行开头添加井号。如果你想在 `inetd.conf` 中添加一个服务器，你需要为其创建一个条目。大多数可以从 `inetd` 运行的服务器都在其文档中包含了示例条目。许多发行版提供的 `inetd.conf` 文件也包含了常见服务器的条目，尽管其中许多已被注释；移除行开头的井号即可激活该服务器。

修改 `inetd.conf` 后，必须重启 `inetd` 超级服务器本身。该超级服务器通常作为标准的 SysV 服务器运行，因此你可以通过输入类似以下内容来重启它：

```bash
# /etc/rc.d/init.d/inetd restart
```

或者，你可以通过向 SysV 启动脚本传递 `reload` 参数（而不是 `restart`）来指示 `inetd` 重新加载其配置。`restart` 选项会关闭服务器然后再次启动它。使用 `reload` 时，服务器不会停止运行；它只是重新读取配置文件并实施任何更改。实际上，两者非常相似。使用 `restart` 更有可能正确实施更改，但也更有可能中断现有连接。

除了使用 SysV 启动脚本，你还可以使用 `kill` 或 `killall`（在阶段 3 中有介绍）向 `inetd` 发送 `SIGHUP` 信号。该信号会导致许多服务器（包括 `inetd`）重新读取其配置文件。例如，如果你知道 `inetd` 的进程 ID（PID），你可以输入 `kill -HUP pid`；或者输入 `killall -HUP inetd` 使所有 `inetd` 实例重新读取其配置文件。（通常，系统上只有一个 `inetd` 实例在运行。）在实践中，这应与 SysV 启动脚本的 `reload` 选项工作方式非常相似——事实上，此类脚本通常使用这种技术来实现该选项。

![](img/f430a19bdf014c43ad7c2d594afd5b21_281_0.png)

> 通常明智的做法是在 `inetd.conf` 中尽可能多地禁用服务器（如果你使用 `xinetd`，则是 `xinetd` 配置文件）。一般原则是，如果你不理解某个服务器的功能，就禁用它。这将通过消除潜在存在漏洞或配置错误的服务器来提高系统的安全性。

## 配置 `xinetd`

`xinetd` 程序是一个扩展的超级服务器。它提供了 `inetd` 的功能，以及类似于 TCP Wrappers 的安全选项。Fedora、Mandriva、Red Hat、openSUSE 以及少数其他现代版本的发行版默认使用 `xinetd`。其他发行版未来可能会使用它。如果你喜欢，你可以将任何发行版中的 `inetd` 替换为 `xinetd`。

`/etc/xinetd.conf` 文件控制 `xinetd`。然而，在默认使用 `xinetd` 的发行版中，该文件仅包含全局默认选项和一条包含存储在 `/etc/xinetd.d` 中文件的指令。每个应通过 `xinetd` 运行的服务器随后会在 `/etc/xinetd.d` 中安装一个包含其自身配置选项的文件。在 `/etc/xinetd.d` 目录中查找名为 `ftp`、`ftpd`、`in.ftpd` 或类似名称的文件。如果存在，你可以编辑此文件以激活你的 FTP 服务器。如果不存在，你可以创建此文件并按照下文描述添加 FTP 条目，或者将此类条目添加到你的 `/etc/xinetd.conf` 文件中。

无论服务的条目是在 `/etc/xinetd.conf` 中还是在 `/etc/xinetd.d` 中的某个文件中，它都包含与 `inetd.conf` 文件类似的信息。不过，`xinetd` 配置文件将信息分散在多行中，并进行了更明确的标记。列表 6.2 展示了一个与之前 `inetd.conf` 条目等效的示例。此条目提供的信息与 `inetd.conf` 条目完全相同，只是它不包含对 `/usr/sbin/tcpd`（TCP Wrappers 二进制文件）的引用。由于 `xinetd` 包含类似的功能，通常不将其与 TCP Wrappers 一起使用。

### 列表 6.2：xinetd 配置条目示例

```
service ftp
{
    socket_type     = stream
    protocol        = tcp
    wait            = no
    user            = root
    server          = /usr/sbin/in.ftpd
    server_args     = -l
}
```

![](img/f430a19bdf014c43ad7c2d594afd5b21_282_0.png)

你现有的 FTP 服务器 `xinetd` 配置文件可能与列表 6.2 不完全相同。如果不相同，最好保留原样，除了 `disable` 选项（下文描述）以及你研究过且确定要修改的其他选项外。

`xinetd` 的一个额外参数很重要：`disable`。如果在服务定义中包含行 `disable = yes`，`xinetd` 将忽略该条目。一些服务器安装在 `/etc/xinetd.d` 中的启动文件默认设置了此选项；你必须编辑该文件并将条目更改为 `disable = no` 才能启用服务器。你还可以通过在主 `xinetd.conf` 文件的 `default` 部分中列出服务器名称来禁用一组服务器，例如在名为 `disabled` 的行中写成 `disabled = ftp shell`。

## 测试您的配置

在完成前面两节描述的更改后，您的 FTP 服务器现在应该已经可以访问了。您可以使用文本模式 `ftp` 程序或 GUI FTP 程序（如 `gftp`）进行测试：

```bash
$ ftp localhost
Connected to localhost (127.0.0.1),
220 www.example.com FTP server (Version 6.4/OpenBSD/Linux-ftpd-0.17) ready.
Name (localhost:rodsmith): rodsmith
334 AUTH SSL OK.
[SSL Cipher AES256-SHA]
331 Password required for rodsmith.
Password:
230-
230 User rodsmith logged in.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp>
```

然后，您可以输入 FTP 命令，例如 `ls`、`cd`、`get`、`put` 和 `exit`。（如果您使用 GUI 客户端进行测试，则使用相应的点击操作代替。）此示例展示了使用 `localhost` 接口连接到计算机的过程。如果成功，这证明服务器正在运行并且本地计算机可以访问它；然而，超级服务器、TCP Wrappers 或 FTP 服务器配置选项可能会限制来自其他计算机的访问。因此，您还应该使用远程计算机以相同的方式进行测试。如果遇到远程访问问题，请检查您的配置文件以寻找限制访问的选项，例如在 `xinetd` 中的 `only_from` 选项，或者如果您使用 TCP Wrappers，检查 `/etc/hosts.allow` 或 `/etc/hosts.deny` 中的任何 FTP 选项。
