
## 命令行选项

命令行选项会覆盖配置文件中的声明。以下是 `sshd` 一些更常用选项的说明。

-   -d (`debug`) 设置调试模式，在此模式下 `sshd` 会将调试信息发送到系统日志，并且服务器保持在前景运行。你可以指定此选项多达三次以增加输出信息的详细程度。另请参阅 `-e`。（`ssh` 客户端使用 `-v` 进行调试；参见第 629 页。）
-   -e (`error`) 将输出发送到标准错误，而不是系统日志。与 `-d` 配合使用时非常有用。
-   -f `file` (`file`) 指定路径名为 `file` 的文件作为默认配置文件，而不是 `/etc/ssh/sshd_config`。
-   -t (`test`) 检查配置文件的语法以及密钥文件的合理性。
-   -D (`noDetach`) 使 `sshd` 保持在前景运行。对调试非常有用；由 `-d` 隐含。

## /etc/ssh/sshd_config 配置文件

`/etc/ssh/sshd_config` 配置文件包含以关键字开头的单行声明，该关键字不区分大小写，后跟空白字符，并以区分大小写的参数结尾。

-   **AllowUsers userlist**

`userlist` 是一个以空格分隔的用户名列表，指定了允许使用 `sshd` 登录的用户。此列表可以包含 `*` 和 `?` 通配符。你可以将用户指定为 `user` 或 `user@host`。如果你使用第二种格式，请确保指定由 `hostname` 返回的主机名。如果没有此声明，任何可以本地登录的用户都可以使用 OpenSSH 客户端登录。

-   **ClientAliveCountMax `n`**

`n` 指定在 `sshd` 断开与客户端的连接之前，可以发送多少条客户端存活消息而不接收响应。参见 `ClientAliveInterval`。默认值为 3。

-   **ClientAliveInterval `n`**

如果在 `n` 秒内未从客户端收到消息，则通过加密通道发送一条消息。参见 `ClientAliveCountMax`。默认值为 0，意味着不发送任何消息。

此声明通过加密通道传递消息，因此不易受到 `IP 欺骗`（第 1089 页）的影响。它与使用 TCP 保活选项且易受 IP 欺骗影响的 `TCPKeepAlive` 不同。

-   **HostbasedAuthentication `yes` | `no`**

当设置为 yes 时，尝试进行 `.rhosts` 身份验证。为了获得更安全的系统，请设置为 no（默认值）。

-   **IgnoreRhosts `yes` | `no`**

忽略用于身份验证的 `.rhosts` 和 `.shosts` 文件。这不影响使用 `/etc/hosts.equiv` 和 `/etc/ssh/shosts.equiv` 文件进行身份验证。为了获得更安全的系统，请设置为 yes（默认值）。

-   **LoginGraceTime *n***

在断开连接之前，等待 *n* 秒让用户在服务器上登录。值为 0 表示没有时间限制。默认值为 120。

-   **LogLevel *val***

指定日志消息的详细程度。从 QUIT、FATAL、ERROR、INFO 和 VERBOSE 中选择 *val*。默认值为 INFO。

-   **PasswordAuthentication**

允许用户使用密码进行身份验证。默认值为 yes。

-   **PermitEmptyPasswords**

允许用户在密码为空的账户上登录。默认值为 no。

-   **Protocol**

指定服务器接受的协议，为 1 和/或 2。如果你想指定两种协议，请用逗号分隔 1 和 2。默认值为 2。有关更多信息，请参阅第 622 页的“SSH1 与 SSH2”。

-   **PermitRootLogin**

允许 *root* 使用 OpenSSH 客户端登录。为了获得更安全的系统，请设置为 no。默认值为 yes。

-   **StrictModes yes | no**

检查用户主目录和文件的模式及所有权。如果目录和/或文件可被任何人写入，则登录失败。为了安全起见，请设置为 yes（默认值）。

-   **TCPKeepAlive yes | no**

当设置为 yes（默认值）时，定期检查连接是否存活。检查操作会在客户端崩溃或连接因其他原因断开时（即使是暂时的）导致 *ssh* 或 *scp* 连接被断开。将此参数设置为 *no* 会导致服务器不检查连接是否存活。

此声明使用 TCP *keepalive* 选项，该选项未加密且易受 *IP 欺骗*（第 1089 页）的影响。请参阅 ClientAliveInterval（第 636 页）了解不可欺骗的替代方案。

-   **X11Forwarding yes | no**

当设置为 yes 时，允许 X11 转发。默认值为 no，但 Fedora/RHEL 将 X11Forwarding 设置为 yes。为了使 X11 转发正常工作，必须在客户端配置文件 `~/.ssh/config` 或 `/etc/ssh/ssh_config`（第 632 页）中将 ForwardX11 声明或 ForwardX11Trusted 声明也设置为 yes。有关更多信息，请参阅第 638 页的“X11 转发”。

## 故障排除

**日志文件**

当你在通过 *ssh* 或 *scp* 连接时遇到问题时，有几个地方可以寻找线索。首先，在服务器上的 /var/log/secure 和 /var/log/messages 中查找 sshd 条目。以下是在使用 AllowUsers 声明但未包含尝试登录的用户时你可能会看到的消息（第 636 页）：

```bash
# grep sshd /var/log/secure
# sshd[16]: User sam not allowed because not listed in AllowUsers
# sshd[16]: Failed password for illegal user sam from 192.168.0.6 port 59276 ssh2
```

下一条消息源自 PAM（第 458 页），表示系统未知该用户：

```bash
# grep sshd /var/log/messages
grape sshd[pam_unix] [2817]: check pass; user unknown
grape sshd[pam_unix] [2817]: authentication failure; logname= uid=0
euid=0 tty=NODEVXs50 ruser= host=peach.sobel1.com
```

**调试客户端**

如果在这些文件中均未找到有助于解决问题的线索，请尝试使用 -v 选项（无论是 ssh 还是 scp——结果应该相同）进行连接。OpenSSH 会显示大量消息，其中一条可能帮助你查明问题所在。

```bash
$ ssh -v grape
OpenSSH_5.2p1, OpenSSL 1.0.0-fips-beta4 10 Nov 2009
debug1: Reading configuration data /etc/ssh/ssh_config
debug1: Applying options for *
debug1: Connecting to grape [192.168.0.3] port 22.
debug1: Connection established.
debug1: identity file /home/sam/.ssh/identity type -1
debug1: identity file /home/sam/.ssh/id_rsa type 1
...
debug1: Host 'grape' is known and matches the RSA host key.
debug1: Found key in /home/sam/.ssh/known_hosts:2
debug1: ssh_rsa_verify: signature correct
...
debug1: Authentications that can continue: publickey,password,keyboard-interactive
debug1: Trying private key: /home/sam/.ssh/id_dsa
debug1: Next authentication method: keyboard-interactive
debug1: Authentications that can continue: publickey,password,keyboard-interactive
debug1: Next authentication method: password
sam@grape's password:
```

**调试服务器**

你可以通过使用 -de 选项运行 sshd 来从服务器端进行调试。服务器将在前景运行，其显示信息可能有助于你解决问题。

## 隧道/端口转发

ssh 工具允许你通过其建立的加密连接转发端口（*端口转发*，第 1099 页）。由于通过转发端口发送的数据使用加密的 ssh 连接作为其数据链路层（第 365 页），因此这类连接被称为隧道（第 1112 页）：“连接通过 ssh 进行隧道传输”。你可以通过 ssh 隧道传输来保护协议——包括 POP、X、IMAP 和 WWW。

### X11 转发

ssh 工具使 X11 协议的隧道传输变得轻而易举。为了使 X11 隧道传输正常工作，你必须在服务器和客户端上都启用它。在服务器上，你通过在 /etc/ssh/sshd_config 文件中将 X11Forwarding 声明设置为 yes 来启用 X11 转发（第 637 页）。

### 可信客户端

过去，客户端启用 X11 转发只有一种方式；如今有两种方式。以前，当你在客户端启用 X11 转发（通过在配置文件中将 ForwardX11 设置为 yes，或在 `ssh` 命令行上使用 `−X` 选项）时，客户端作为可信客户端连接，这意味着客户端信任服务器，并获得对 X11 显示的完全访问权限。如果拥有对 X11 显示的完全访问权限，在某些情况下，客户端可能能够修改 X 显示的其他客户端。只有在你信任远程系统时，才建立安全连接。（你不想有人篡改你的客户端。）如果这个概念令人困惑，请参阅第 257 页的技巧“X 客户端和服务器的角色可能违背直觉”。

从 Fedora Core 3 和 RHEL 版本 4（OpenSSH 3.8 及更高版本）开始，`ssh` 客户端可以作为可信客户端或非可信客户端连接到 `ssh` 服务器。非可信客户端仅获得对 X11 显示的有限访问权限，并且不能修改 X 显示的其他客户端。

少数客户端在非可信模式下能正常工作。如果你正在非可信模式下运行 X 客户端并遇到问题的，请尝试在可信模式下运行（假设你信任远程系统）。Fedora/RHEL 默认配置 `ssh` 客户端以可信模式运行。

## 运行 ssh

当你启动 `ssh` 客户端时，可以使用命令行上的 `−Y` 选项（第 629 页）以可信模式启动客户端。此选项执行与早期版本 `ssh` 中 `−X` 选项相同的功能。或者，你可以将 ForwardX11Trusted 声明设置为用户 `~/.ssh/config` 配置文件（第 632 页）中的 `yes`；或者，以 `root` 身份工作时，你可以将 ForwardX11Trusted 设置为全局 `/etc/ssh/ssh_config` 文件（第 632 页）中的 `yes` 以启用可信的 X11 隧道传输。

要使用非可信隧道传输，你可以使用 `−X` 选项（第 629 页），或在一个配置文件中将 ForwardX11 声明设置为 `yes`（第 632 页）。

在开启 X11 转发的情况下，`ssh` 会对 X11 协议进行隧道传输，设置所连接系统上的 DISPLAY 环境变量并转发所需的端口。你必须设置 DISPLAY 变量。通常你会从 GUI 运行，这通常意味着你正在使用终端模拟器通过 `ssh` 连接到远程系统。当你在 `ssh` 提示符下给出 X11 命令时，OpenSSH 会创建一个新的安全通道来承载 X11 数据。X11 程序的图形输出将显示在你的屏幕上。

```bash
[peach]$ ssh speedy
[speedy]$ echo $DISPLAY
localhost:10.0
```

默认情况下，`sshd` 使用 X Window System 显示编号 10 及以上（端口号 6010 及以上）用于转发的 X 会话。一旦你使用 `ssh` 连接到远程系统，你就可以输入命令来运行 X 应用程序。该应用程序将在远程系统上运行，其显示出现在本地系统上，从而看起来像是在本地运行。

## 端口转发

你可以使用 `−L` 和 `−R` 选项转发任意端口。`−L` 选项将本地端口转发到远程系统，使得尝试连接本地系统中转发端口的程序可以透明地连接到远程系统。`−R` 选项执行相反操作：它将远程端口转发到本地系统。`−N`

