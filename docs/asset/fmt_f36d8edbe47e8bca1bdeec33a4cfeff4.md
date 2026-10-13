
进入`/path/to/xxx`目录，找到`xxx.json`。

- 更新软件：Fedora Core 的`up2date`和`Yum`工具可以帮助计算机软件保持最新，从而在漏洞被发现时消除它们。

- 移除服务：如果不使用某些软件，黑客就无法利用其漏洞。关闭不必要的服务可以减少风险。您可能还想从服务器上卸载某些软件，如编译器。移除软件可以防止黑客利用它们。

- OpenSSH 和 SSL：除非您正在查看普通的非 Web 页面，否则永远不要在不使用加密的情况下通过互联网或无线局域网进行通信。开源 SecureShell `SSH` 和安全套接层 `SSL` 为您的通信提供了有效的加密。

我们将描述本节中的每种系统。

# 第 17 章：守护您的未来

## 更新软件以消除漏洞

黑客的标准操作程序非常简单：发现并利用漏洞。这种方法简单却有效，其原理如下：黑客 Joe 在互联网上到处走动，拉拉门手，偶尔发现一些没锁的门。当没有门没锁时，黑客会寻找更容易进入的门。您的任务是确保门是锁好的且安全的。

运行防火墙、关闭不必要的服务并使用良好的密码，可以确保您不会留下任何未锁的状态。

## 保障您的未来

此示例每天凌晨 1 点启动`up2date`实用程序。该选项强制`up2date`更新任何可用的 Fedora Core 软件包。

定期更新您的计算机是一项至关重要且易于操作的安全措施。许多入侵事件都是由于软件过旧导致的。在`up2date`的帮助下，你可以在漏洞发生时就消除大多数漏洞。

## 减少您的暴露：移除和减少服务

黑客通过探测易受攻击的网络服务来寻找计算机漏洞。网络服务——例如`Apache`、`Samba`和`DHCP`——无疑是为了设计响应网络查询而设计的。因此，黑客可以识别出你运行了哪些服务，并找到可以使用哪些攻击方法。

我们在其他地方描述了保持软件更新如何降低你的易脆弱性。然而，你可以更进一步，通过关闭服务来使其变得不再脆弱。一个简单的安全规则是“保持简单”。事实是，如果你不需要运行某个服务，就不应该运行它。

在本节中，我们将描述如何消除或减少网络和非网络服务。这些步骤描述了如何使用`chkconfig`工具更改启动脚本，这些脚本控制着网络服务在启动时何时、如何以及是否启动：

1. 点击 GNU 菜单并选择系统设置 `System Settings` -> 服务器设置 `Server Settings` -> 如果提示，输入 root 密码。

打开服务配置 `Service Configuration` 对话框。

2. 选择一个不需要的服务并点击停止 `Stop` 按钮将其关闭。

3. 当确认对话框出现时，点击 `OK` 按钮。

4. 点击服务左侧的勾选以取消勾选。

取消勾选可以防止服务在启动时自动启动。

5. 对每个不需要的服务重复步骤 2–4。

6. 当你关闭了每个不需要的服务后，点击保存 `Save` 按钮。

7. 从文件 `File` 菜单中选择退出 `Quit`。

关闭哪些服务取决于你的需求。例如，如果你在无意中运行了 Web 服务器，请关闭`httpd`服务。你通常应该能够关闭这些服务：

高级电源管理守护进程 `APMD`：如果你像大多数人一样定期关闭你的个人工作站或笔记本电脑，那么`APMD`是有用的。然而，对于持续运行的服务器，`APMD`通常是不必要的。在一种情况下工作站或笔记本电脑你想要保留`APMD`，而在另一种情况下服务器应将其移除。

- `GPM`：此服务允许你在非图形界面模式下使用鼠标。你正在运行图形界面模式，因此请将其关闭。

- 任务队列守护进程：`atd`守护进程用于调度一次性 cron 任务。如果你需要它，你自然会知道。否则，请将其关闭。

- 网络文件共享 `NFS`：当你运行 NFS 服务器或客户端时，你只需要`nfs`、`nfslock`、`portmap`和`autofs`等服务。你最不想做的一件事就是将文件共享到互联网上。

- 打印服务：许多人不会在服务器上运行打印机守护进程。当你不需要打印时，请关闭`CUPS`通用 UNIX 打印系统或`lpd`。

- `Samba`：就像 NFS 一样，如果你不需要`Samba`，就应该关闭它。

剩下的取决于你。以严厉之击终结黑客的行为。

当服务未运行时，你无法对其进行修改。你可以切换未运行服务的勾选状态，但如果它没有运行，这种操作不会产生任何影响。

你可以使用基于 CLI 的`chkconfig`工具。打开一个 Gnome Terminal 会话并以 root 身份登录 `su -`。这列出了你的选项：

- 运行`chkconfig --list`命令列出服务。

- 在`--list`选项后指定服务以列出单个服务：`chkconfig --list apmd`。

- 使用`--add`选项停止服务：`chkconfig --add apmd`。

- 使用`--delete`选项删除服务：`chkconfig --delete apmd`。

3. 输入你的用户名和密码。

4. 在`sftp`提示符处输入帮助命令。

你会看到一个`sftp`命令列表。你最常用的命令是`cd`、`lcd`、`dir`、`ls`、`get`和`put`。这些命令用法与 Linux 命令类似。

使用`sftp`是显而易懂的。使用`get`将文件、文件或目录从远程机器传输到本地机器；使用`put`从本地传输到远程。

OpenSSH 的另一个酷功能是它能够对任何协议进行隧道传输。例如，你可以通过 X 从远程机器显示整个 X 窗口。更多信息请参阅 OpenSSH 文档。

![](img/85ec3de0d5219d6ca14d5778e16a3338_268_0.png)

## 配置 OpenSSH 服务器

配置 OpenSSH 服务器非常简单。你只需要修改`/etc/ssh/sshd_config`文件并运行`/etc/init.d/sshd`脚本。查看该配置文件，其重要部分列在以下符号中：

- 移除旧且有错误的协议版本：版本 1 是损坏的，不应使用，如示例所示，将参数`Protocol 2,1`改为`Protocol 2`：

```bash
Port 22
Protocol 2
## HostKeys for protocol version 2
HostKey /etc/ssh/ssh_host_rsa_key
HostKey /etc/ssh/ssh_host_dsa_key
```

- 移除登录超时时间参数前的注释：此操作设置了从开始登录到完成登录之间的时间限制：

```bash
LoginGraceTime 600
```

- 不允许 root 登录：你应该防止用户包括你自己直接以 root 身份登录。强制用户先以普通用户身份登录，然后`su`切换到 root，这样可以提供审计追踪，用于查看是谁以 root 用户身份做了什么；它还强迫每个人在成为全能的 root 用户之前经过两个关卡：

```bash
PermitRootLogin yes
StrictModes yes
```

- 取消这些的注释允许各种认证模式：

  - 不应使用 hosts 认证

    `RhostsAuthentication no`

  - 不要读取用户的`~/.hosts`和`~/.shosts`文件

    `IgnoreHosts yes`

  - 要使此项生效，你还需要在`/etc/ssh/ssh_known_hosts`中有主机密钥

    `RhostsRSA no`

  - 协议版本 2 类似

    `HostbasedAuthentication no`

  - 如果你不信任`~/.ssh/known_hosts`用于`RhostsRSAAuthentication`和`HostbasedAuthentication`，则将其改为 yes

    `IgnoreKnownHosts no`

- 允许策略使用密码认证，但不允许未验证的访问：

  - 要禁用隧道明文密码，请在此处改为 no！

```bash
PasswordAuthentication yes
PermitEmptyPasswords no
```

要启动 OpenSSH 守护进程，请遵循以下步骤：

1. 更改并重启 Secure Shell 守护进程：

   `/etc/init.d/sshd restart`

2. 如果你正在运行防火墙，请向基于 iptables 的防火墙添加此规则：

   `iptables -A INPUT -p tcp --port 22 -m state --state NEW,ESTABLISHED -j ACCEPT`

3. 保存你的新防火墙：

   `iptables-save > /etc/sysconfig/iptables`

4. 重启防火墙：

   `/etc/init.d/iptables restart`
