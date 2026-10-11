
`inetd` 和 `xinetd` 的一个安全特性是它们使用 `TCP wrapper` 来启动各种服务。`TCP wrapper` 是一段代码，它为 Internet 服务提供访问控制设施，就像您的消息的保护包装一样。`TCP wrapper` 可以启动其他服务，例如 FTP 和 TELNET；但在启动服务之前，它会查阅 `/etc/hosts.allow` 文件，查看请求服务的宿主是否被允许使用该服务。如果 `/etc/hosts.allow` 中没有关于该宿主的信息，`TCP wrapper` 会检查 `/etc/hosts.deny` 文件，查看是否拒绝该服务。如果两个文件都为空，`TCP wrapper` 将提供对请求服务的访问。

以下是收紧 `inetd` 或 `xinetd` 配置启动的服务访问权限的步骤：

1. 使用文本编辑器编辑 `/etc/hosts.deny` 文件，向该文件添加以下行：

```
ALL:ALL
```

此设置拒绝所有宿主访问您系统上的任何 Internet 服务。

2. 编辑 `/etc/hosts.allow` 文件，并添加可以访问您系统上服务的宿主名称。

例如，要使仅 192.168.1.0 网络的宿主和本地主机（IP 地址 127.0.0.1）能够访问您系统上的服务，请将以下行放在 `/etc/hosts.allow` 文件中：

```
ALL: 192.168.1.0/255.255.255.0 127.0.0.1
```

3. 如果您希望允许特定的远程宿主访问特定的 Internet 服务，您可以使用 `/etc/hosts.allow` 中某行的以下语法来实现：

```
server_program_name: hosts
```

这里，`server_program_name` 是服务器程序的名称，而 `hosts` 是可以访问该服务的宿主列表（以逗号分隔）。

您也可以将 `hosts` 写为网络地址或整个域名，例如 `.mycompany.com`。

### 使用安全外壳 (SSH) 进行远程登录

Linux 附带 Open Secure Shell (OpenSSH) 软件，这是一组程序，为 Berkeley r 命令提供了安全的替代方案：`rlogin`（远程登录）、`rsh`（远程 shell）和 `rcp`（远程复制）。OpenSSH 使用公钥密码学对用户进行身份验证，并对两台主机之间的通信进行加密，因此用户可以安全地从远程系统登录并安全地复制文件。

在本节中，我将简要描述如何在 Linux 中使用 OpenSSH 软件。要了解有关 OpenSSH 的更多信息并阅读最新新闻，请访问 www.openssh.com 或 www.openssh.org。

OpenSSH 软件在 Linux 安装期间已安装。表 3-1 列出了 OpenSSH 软件的主要组件。

表 3-1 OpenSSH 软件的组件

| 组件 | 描述 |
|---|---|
| `/usr/sbin/sshd` | 此 Secure Shell 守护程序必须在主机上运行，如果您希望远程系统上的用户能够使用 `ssh` 客户端安全登录。当来自 `ssh` 客户端的连接到达时，`sshd` 使用公钥密码学执行身份验证，并与 `ssh` 客户端建立加密通信链路。 |
| `/usr/bin/ssh` | 用户可以运行此 Secure Shell 客户端登录到运行 `sshd` 的主机。用户也可以使用 `ssh` 在另一台主机上执行命令。 |

## 使用安全 shell (SSH) 进行远程登录

| 组件 | 描述 |
| :--- | :--- |
| `/usr/bin/login` | 指向 `/usr/bin/ssh` 的符号链接 |
| `/usr/bin/scp` | 安全工作 like `scp` 的 secure-copy 程序。`scp` 程序使用 `ssh` 进行数据传输，并提供与 `ssh` 相同的认证和安全机制。 |
| `/usr/bin/ssh-keygen` | 使用此程序生成在 OpenSSH 中用于公钥密码术所需的公钥和私钥对。`ssh-keygen` 程序可以为 RSA 和 DSA（数字签名算法）认证生成密钥对。（RSA 算法的名称源自罗恩·李维斯特（Ron Rivest）、阿迪·沙米尔（Adi Shamir）和伦纳德·阿德勒曼（Leonard Adleman）——该算法开发者的姓名首字母。） |
| `/etc/ssh/sshd_config` | 此 `sshd` 服务器的配置文件指定了 `sshd` 的许多参数——包括监听的端口、使用的协议以及其他文件的位置。（SSH 协议有两个版本，SSH1 和 SSH2，OpenSSH 均支持这两种版本。） |
| `/etc/ssh/ssh_config` | 此配置文件用于 `ssh` 客户端。每个用户也可以在用户主目录的 `.ssh` 子目录中拥有一个名为 `config` 的 `ssh` 配置文件。 |

OpenSSH 使用公钥加密，其中发送方和接收方都拥有一对密钥——一个公钥和一个私钥。公钥可以自由分发，且各方都知道对方的公钥。发送方使用接收方的公钥加密数据。只有接收方的私钥才能解密该数据。

要使用 OpenSSH，首先需要启动 `sshd` 服务器，然后生成主机密钥。方法如下：

- 如果你想在主机上支持基于 SSH 的远程登录，请在你的系统上启动 `sshd` 服务器。输入 `ps ax | grep sshd` 以查看服务器是否已在运行。如果没有，请以 root 身份登录并启动 SSH 服务。
- 在 Fedora Core 和 SUSE 中，输入 `chkconfig --level 35 sshd on`。在 Debian 和 Xandros 中，输入 `update-rc.d ssh defaults`。若要立即启动 `sshd` 服务器，在 Debian 和 Xandros 中输入 `/etc/init.d/ssh start`，或在 Fedora Core 和 SUSE 中输入 `/etc/init.d/ssh start`。

使用以下命令生成主机密钥：

```
ssh-keygen -d -f /etc/ssh/ssh_host_key -N ''
```

`-d` 标志使 `ssh-keygen` 程序生成 DSA 密钥，这是 SSH2 协议所使用的。如果你看到一条消息说文件 `/etc/ssh/ssh_host_key` 已经存在，这意味着密钥对在 Linux 安装过程中已生成。你可以使用现有文件，而无需重新生成密钥。

![](img/11709a8f88c8cd03868a929dc94c0e2b_558_0.png)

![](img/11709a8f88c8cd03868a929dc94c0e2b_558_1.png)

希望使用 SSH 登录的用户可以简单地使用 `ssh` 命令。例如，这是我在一个系统上输入以通过 SSH 登录到另一个系统的命令：

```
ssh 192.168.0.4 -l naba
```

其中 192.168.0.4 是另一个 Linux 系统的 IP 地址。然后 SSH 显示一条消息：

> 无法确定主机 '192.168.0.4 (192.168.0.4)' 的真实性。
> RSA 密钥指纹为 7b:79:f2:d3:8c:54:00:a6:94:ec:fa:8e:7f:c9:ad:66。
> 你确定要继续连接吗 (yes/no)？

我输入 yes 并按 Enter。然后 SSH 将该主机添加到其已知主机列表，并提示我输入另一个 Linux 系统的密码：

```
naba@192.168.0.4's password:
```

输入密码后，我即与该系统建立了安全的登录会话。我也可以使用以下等效命令登录到此账户：

```
ssh naba@192.168.0.4
```

如果我只想从局域网（LAN）上的另一个系统（由其 IP 地址 192.168.0.4 标识）安全地复制文件，可以这样使用 `scp`：

```
scp 192.168.0.4:/etc/X11/xorg.conf .
```

此命令提示输入我的密码，并将 `/etc/X11/xorg.conf` 文件从 192.168.0.4 主机安全地复制到输入 `scp` 命令的系统，如下所示：

```
naba@192.168.0.4's password: (我输入密码。)
xorg.conf             100% 2814      2.8KB/s   00:00
```

### 设置简单防火墙

防火墙是一个具有两个或更多网络接口的网络设备或主机——一个连接到受保护的内部网络，另一个连接到未受保护的网络（如互联网）。防火墙控制对受保护内部网络的访问。
