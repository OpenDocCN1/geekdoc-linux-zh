
除了像 Web 服务器或邮件服务器这样的独立服务器外，还有 `inetd` 或 `xinetd` 等其他服务器，你必须单独配置它们。这些服务器被称为互联网超级服务器，因为它们可以按需启动其他服务器。

输入 `ps ax | grep inetd` 以查看你的系统运行的是哪种互联网超级服务器——`inetd` 或 `xinetd`。

Debian、MEPIS、Ubuntu 和 Xandros 使用 `inetd`，而 Fedora Core 和 SUSE 使用 `xinetd`。

`inetd` 服务器通过 `/etc/inetd.conf` 文件进行配置。你可以通过在该文件中找到相应的行并在行首添加井号 `#` 来注释掉该行使服务失效。保存配置文件后，输入 `/etc/init.d/inetd restart` 以重启 `inetd` 服务器。

配置 `xinetd` 服务器稍微复杂一些。`xinetd` 服务器在启动时读取名为 `/etc/xinetd.conf` 的配置文件。该文件转而引用存储在 `/etc/xinetd.d` 目录中的配置文件。`/etc/xinetd.d` 中的配置文件告诉 `xinetd` 监听哪些端口以及为每个端口启动哪个服务器。输入 `ls /etc/xinetd.d` 以查看你系统上 `/etc/xinetd.d` 目录中的文件列表。每个文件代表 `xinetd` 可以启动的一项服务。要关闭其中任何服务，请在文本编辑器中编辑该文件并在文件中添加 `disable = yes` 行。在对 `xinetd` 配置文件进行任何更改后，你必须重启 `xinetd` 服务器；否则，更改不会生效。要重启 `xinetd` 服务器，请输入 `/etc/init.d/xinetd restart`。此命令停止 `xinetd` 服务器，然后再次启动它。重启时，它读取配置文件，更改将生效。

### 配置 `TCP wrapper` 安全

`inetd` 和 `xinetd` 的一项安全功能是它们使用 `TCP wrapper` 启动各种服务。`TCP wrapper` 是一段代码，为互联网服务提供访问控制机制，充当你信息的保护包。`TCP wrapper` 可以启动其他服务，如 FTP 和 TELNET；但在启动服务之前，它会查阅 `/etc/hosts.allow` 文件，查看请求服务的宿主是否被允许使用该服务。如果 `/etc/hosts.allow` 中没有关于该宿主的信息，`TCP wrapper` 会检查 `/etc/hosts.deny` 文件，看是否拒绝该服务。如果两个文件都为空，`TCP wrapper` 将提供对所请求服务的访问。

以下是收紧 `inetd` 或 `xinetd` 配置启动的服务访问权限的步骤：

1. 使用文本编辑器编辑 `/etc/hosts.deny` 文件，将以下行添加到该文件中：

```
ALL:ALL
```

此设置拒绝所有宿主访问你系统上的任何互联网服务。

2. 编辑 `/etc/hosts.allow` 文件，并添加可以访问你系统服务的宿主名称。

例如，要仅允许来自 192.168.1.0 网络的宿主和本地主机（IP 地址 127.0.0.1）访问你系统上的服务，请将以下行放在 `/etc/hosts.allow` 文件中：

`ALL: 192.168.1.0/255.255.255.0 127.0.0.1`

3. 如果你希望允许特定远程宿主访问特定互联网服务，可以使用 `/etc/hosts.allow` 中行的以下语法来实现：

`server_program_name: hosts`

这里，`server_program_name` 是服务器程序的名称，`hosts` 是可以访问该服务的宿主逗号分隔列表。你也可以将 `hosts` 写为网络地址或整个域名，例如 `.mycompany.com`。

## 使用安全外壳协议（SSH）进行远程登录

Linux 附带 Open Secure Shell（OpenSSH）软件，这是一套为 Berkeley r 命令提供安全替代方案的程序：`rlogin`（远程登录）、`rsh`（远程 shell）和 `rcp`（远程复制）。OpenSSH 使用公钥加密来验证用户身份并加密两个宿主之间的通信，因此用户可以从远程系统安全登录并安全地复制文件。

在本节中，我将简要描述如何在 Linux 中使用 OpenSSH 软件。要了解有关 OpenSSH 的更多信息并阅读其最新新闻，请访问 www.openssh.com 或 www.openssh.org。

OpenSSH 软件在 Linux 安装期间安装。表 3-1 列出了 OpenSSH 软件的主要组件。

**表 3-1 OpenSSH 软件的组件**

| 组件 | 描述 |
| :--- | :--- |
| `/usr/sbin/sshd` | 如果你想让远程系统上的用户使用 `ssh` 客户端安全登录，此 Secure Shell 守护进程必须在宿主上运行。当来自 `ssh` 客户端的连接到达时，`sshd` 使用公钥加密执行身份验证，并与 `ssh` 客户端建立加密通信链接。 |
| `/usr/bin/ssh` | 用户可以运行此 Secure Shell 客户端登录到正在运行 `sshd` 的宿主。用户还可以使用 `ssh` 在另一个宿主上执行命令。 |
| `/usr/bin/login` | 指向 `/usr/bin/ssh` 的符号链接 |
| `/usr/bin/scp` | 安全工作类似 `scp` 的安全复制程序。`scp` 程序使用 `ssh` 进行数据传输，并提供与 `ssh` 相同的身份验证和安全功能。 |
| `/usr/bin/ssh-keygen` | 使用此程序生成 OpenSSH 中使用的公钥加密所需的公钥和私钥对。`ssh-keygen` 程序可以为 RSA 和 DSA（数字签名算法）身份验证生成密钥对。（RSA 算法的名称取自该算法开发者 Ron Rivest、Adi Shamir 和 Leonard Adleman 的姓名首字母。） |
| `/etc/ssh/sshd_config` | 此 `sshd` 服务器的配置文件指定了 `sshd` 的许多参数——包括要监听的端口、使用的协议以及其他文件的位置。（SSH 协议有两个版本，SSH1 和 SSH2，OpenSSH 均支持这两种版本。） |
| `/etc/ssh/ssh_config` | 此配置文件用于 `ssh` 客户端。每个用户也可以在用户主目录的 `.ssh` 子目录中拥有一个名为 `config` 的 `ssh` 配置文件。 |

OpenSSH 使用公钥加密，其中发送方和接收方都拥有一对密钥——一个公钥和一个私钥。公钥是自由分发的，且每一方都知道对方的公钥。发送方使用接收方的公钥对数据进行加密。然后，只有接收方的私钥才能解密数据。

要使用 OpenSSH，首先需要启动 `sshd` 服务器，然后生成主机密钥。操作方法如下：

- 如果要在主机上支持基于 SSH 的远程登录，请在系统上启动 `sshd` 服务器。输入 `ps ax | grep sshd` 查看服务器是否已在运行。如果没有，请以 root 身份登录并启用 SSH 服务。

- 在 Fedora Core 和 SUSE 中，输入 `chkconfig -level 35 sshd on`。在 Debian 和 Xandros 中，输入 `update-rc.d ssh defaults`。若要立即启动 `sshd` 服务器，请在 Debian 和 Xandros 中输入 `/etc/init.d/ssh start`，或在 Fedora Core 和 SUSE 中输入 `/etc/init.d/ssh start`。

- 使用以下命令生成主机密钥：

```
ssh-keygen -d -f /etc/ssh/ssh_host_key -N ''
```

`-d` 标志使 `ssh-keygen` 程序生成 DSA 密钥，这是 SSH2 协议所使用的。如果看到提示文件 `/etc/ssh/ssh_host_key` 已存在的消息，这意味着密钥对在 Linux 安装过程中已生成。你可以直接使用现有文件，无需重新生成密钥。

![](img/792720823146d68f19fd50c99ebfce4b_558_0.png)

第六卷

第 3 章

提高网络安全

想要使用 SSH 登录的用户可以简单地使用 `ssh` 命令。例如，这是在系统上输入的命令，用于通过 SSH 登录到另一个系统：

```
ssh 192.168.0.4 -l naba
```

其中 192.168.0.4 是另一个 Linux 系统的 IP 地址。然后 SSH 显示一条消息：

> 无法验证主机 '192.168.0.4 (192.168.0.4)' 的真实性。
> RSA 密钥指纹为 7b:79:f2:d8:8c:54:00:a6:94:ec:fa:8e:7f:c9:ad:66。
> 你确定要继续连接吗 (yes/no)?

输入 yes 并按 Enter。然后 SSH 将该主机添加到其已知主机列表中，并提示输入另一个 Linux 系统上的密码：
