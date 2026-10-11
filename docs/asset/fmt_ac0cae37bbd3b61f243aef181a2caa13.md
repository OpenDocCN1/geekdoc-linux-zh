
SSH 在“华丽度”上的缺失通过纯粹的实用性得到了弥补。对于管理员来说，一个到远程主机的安全加密会话是无价的，而且由于 Linux 以命令行为向的设计，几乎不需要其他的远程访问。设置 SSH 非常简单。首先从安装 SSH 守护进程 (`sshd`) 开始。很有可能它已经安装了，因为大多数发行版默认都包含了它。应该配置一些命令行选项来影响守护进程的安全和运行。这并不是完整的选项列表，仅是从安全角度来看最重要的几个：

- `-f <configuration_file>` 指定配置文件；如果不指定配置文件，`sshd` 将不会启动。
- `-h <host_key_file>` 此选项指定包含主机密钥的文件。如果 `sshd` 不是以 root 身份运行，则你必须使用此选项。由于 `sshd` 可以在不以 root 身份运行时工作，请将其配置为非 root 账户并使用此选项。

下一步是为 `sshd` 创建配置文件，如果你没有使用 `-f` 选项指定替代路径，则默认为 `/etc/ssh_config`。以下是关键字的列表列表，仅包含最重要的安全设置。关键字和参数是对大小敏感的：

- `AllowGroups` 根据用户组名指定允许登录的组。支持通配符。默认是所有组。你应该创建一个专门针对 `sshd` 用户的组并进行适当的填充。
- `AllowUsers` 根据用户名指定允许登录的用户。默认是允许所有用户。你也可以指定 `USER@HOST` 以允许特定用户仅从特定机器登录。
- `Banner` 是一条典型的横幅消息，通常设置一些经过法律部门批准的阴森警告消息是个好主意。此消息在客户端登录之前发送给客户端，仅在 `sshd` V2 支持。
- `ClientAliveInterval` 指定了 `sshd` 向客户端发送消息请求响应之前，会话可以空闲的时间。默认值为 0，这意味着客户端永远不会看到这些请求，随后永远不会被断开（见下文）。此设置实际上不会断开客户端。
- `ClientAliveCountMax` 指定了在客户端断开之前，可以向客户端发送多少个响应请求而未收到响应。默认值为 3，因此如果将 `ClientAliveInterval` 设置为 20，则无响应的客户端将在 60 秒后被断开。
- `KeyRegenerationInterval` 指定了重新生成服务器密钥的频率。如果资源允许，取决于你想多大偏执，越低的设置越安全。
- `LoginGraceTime` 指定了守护进程等待客户端进行身份验证的时间。默认是 600 秒，这太长了，简直是在招揽拒绝服务 (`DoS`) 攻击。将其设置为较小的数字，例如 30 秒或更短。
- `PrintMotd` 这将在用户登录后打印 `/etc/motd`。之前描述的 `Banner` 选项也适用于某些考虑。

一旦你有了配置文件并使用所有适当选项启动了 `sshd` 守护进程，你就可以允许 `ssh` 监听端口（默认是 TCP22）上的入站连接。使用基于 GUI 的工具（如安全级别配置实用程序）非常简单。导航到 System | Administration | Security Level and Firewall。在“Trusted Services”旁边的“Firewall Options” 选项卡中，在 SSH 旁边打勾选。我们之前在图 14.9 中展示过这一点。完成后，点击 OK，当警告对话框出现时再次点击 OK。

```bash
iptables -A INPUT -p tcp -m state --state NEW --dport 22 -j ACCEPT
```

## 远程 GUI

尽管你可以通过 SSH 完成任何任务，但也许你更习惯使用 GUI。明显的问题是，如何访问 GUI？通常有两种方法：使用内置功能或使用专门为共享桌面设计的第三方软件。无论哪种情况，你都必须加密会话。免费版的 VNC 使用初始挑战响应来隐藏密码，但之后会话是完全不加密的。付费版本支持加密。另一种商业选择是 NoMachine NX 服务器。

`Cygwin/X` 是一个为 Windows 提供运行 X 客户端和 SSH 客户端的免费软件包。首先，你需要在 Linux 主机上开放 SSH 的入站端口。SSH 默认端口是 TCP 22。

X Server 还有自己的安全机制。你必须有一个允许连接到 X Server 的用户名和机器列表。此列表使用 `xhost` 工具进行修改。过程非常简单：输入 `xhost+bob` 将用户或机器添加到允许列表中。输入 `xhost-bob` 将其从列表中删除。最后，你需要确保 `ssh_config` 必须将 `ForwardX11` 设置为 `Yes`，以允许 X Server 通过 SSH 工作，在大多数情况下它应该默认为 `On`。

### Web 服务器配置

2. 配置防火墙以分别允许入站端口 80 和 443 对应的 HTTP 和 HTTPS 连接。你可以通过输入 `iptables -L` 列出链来验证端口是否已允许。应该会有类似下面的几行：

| ACCEPT | tcp | anywhere | start NEW tcp dpt:https |
| ACCEPT | tcp | anywhere | start NEW tcp dpt:http |

3. 如果你托管了一个域名，你将要把域名和你的服务器地址添加到 `/etc/hosts` 文件中。

4. Apache 使用配置文件来确定它如何处理网站。你应该访问 http://apache.org/docs/2.0/ 阅读可用文档以获取更多信息。该文件默认位于 `/etc/httpd/http.conf`。如有需要，编辑此文件。

5. 假设你想让 `httpd` 自动启动，请前往 System | Administration | Services，并在相应的运行级别下在 `httpd` 旁边打上勾选框。

6. 如果需要，为日志文件配置适当的监控（如 `swatch`）。日志文件的默认位置是 `/etc/httpd/logs/`。

7. 此时，你应该能够连接到 Web 服务器并看到 Apache 测试页面。下一步是配置 HTTPS。你可以向 `/var/www/html` 添加你自己的内容，并将权限设置为适用于 Web 访问的权限，通常是读取；如果使用了脚本，则为读取和执行；例如：`chown -R 755 /var/www/html`。

8. 安装 `mod_ssl`（Apache 的 SSL/TLS 模块）和 `openssl`。

9. 将你的 SSL 证书（从第三方 CA 获取）放置在你选择的目录中，并编辑 `/etc/httpconf/httpd.conf` 文件以包含以下行，这些行指向证书文件。你应该使用安全的根分区来存放你的证书文件。

```
SSLCertificateFile <path to certificate file>/server.crt
SSLCertificateKeyFile <path to certificate file>/server.key
```

10. 修改权限以确保服务器文件仅对 root 可。

## 配置 FTP 服务器

要将你的堡垒机配置为 FTP 服务器，请遵循以下步骤：

- 1. 选择并安装 FTP 服务器守护进程。两个很好的选择是 `vsftpd` 和 `pure-ftpd`，但还有许多其他可供选择。如果你正在使用 SELinux，`pure-ftpd` 包含了 SELlinux 支持，但必须单独下载。一些用户报告 `vsftpd` 的性能更好，因此我们将在此示例中使用它；更多信息请访问 http://vsftpd.beats.org/ 上的 `vsftpd` 网站。
- 安装守护进程后，确保该服务被设置为在相应的运行级别下自动启动。
- 在防火墙上启用 FTP 入站支持，TCP 端口 21。此时，你应该能够从远程主机连接到 FTP 服务器。
- 编辑位于 `/etc/vsftp/vsftpd.conf` 的 `vsftd` 配置文件（必须由 root 所有）。以下是一些需要注意的更以安全为导的设置。`vsftpd` 的默认设置是安全的。
- `anonymous_enable`：默认是 Yes，如果你注释掉这一行，默认仍然是匿名的，除非你将其设置为 No。
- `ssl_enable`：应设置为 Yes 以使用 SSL 加密传输。
- `dual_log_enable`：将此项设置为 Yes。它告诉 `vsftpd` 在 `/var/log/vsftpd.log` 之外还生成 FTP 格式的日志（`/var/log/xferlog`）。更多解析工具可以识别 FTP 格式的日志。
- `force_local_logins`：将此项设置为 Yes 将允许所有匿名登录使用 SSL。
- `syslog_enable`：将此项设置为 Yes 会将日志写入系统日志。
- `tcp_wrappers`：将此项设置为 Yes 将启用 tcp_wrapper 支持（`vsftpd` 必须编译了 tcp_wrapper 支持才能生效）。
- `userlist_deny`：此选项仅在 `userlist_enable` 设置为 Yes 时使用。将此选项设置为 No 意味着除非用户在用户列表文件 `/etc/vsftpd/user_list` 中显式列出，否则将被拒绝登录。还需要注意，用户在提示之前就会被拒绝。
