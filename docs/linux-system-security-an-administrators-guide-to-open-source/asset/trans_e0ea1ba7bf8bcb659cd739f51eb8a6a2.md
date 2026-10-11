

## 表 11.5 /etc/ssh/sshd_config 中的关键字（续）

| 关键字 | 描述 |
| :--- | :--- |
| PermitEmptyPasswords | 如果为 yes（默认值），则允许没有密码的用户通过 sshd 进行身份验证。如果为 no，则 sshd 不允许使用空密码。 |
| PermitRootLogin | 如果为 yes（默认值），则允许 root 用户登录。如果为 no，则 root 用户无需提供 root 的密码，但在此情况下必须通过三种非密码身份验证机制之一进行身份验证。否则，no pwd 的行为类似于 no，完全禁止 root 登录。例外情况是，如果启用并配置了 RSA 身份验证，root 用户可以通过 ssh 执行命令。 |
| PidFile | 包含主 sshd 进程 PID 的文件位置。默认为 /var/run/sshd.pid。 |
| Port | 指定 sshd 绑定的端口号。默认为 22。 |
| PrintMotd | 如果为 yes（默认值），则在登录后显示 /etc/motd 文件。 |
| QuietMode | 如果为 no，则抑制除致命错误以外的所有日志记录。通常，初始连接请求、身份验证信息和连接终止信息会通过 syslog 设施 DAEMON 记录。有关配置选项，请参见本表中的 SyslogFacility 关键字。默认为 yes。如果指定了 -q 命令行选项，此关键字将被覆盖。 |
| RandomSeed | 指定包含服务器随机种子的文件。默认为 /etc/ssh_random_seed；RPM 包中的默认为 /etc/ssh/ssh_random_seed。 |
| RhostsAuthentication | 如果为 yes，则允许 Rhosts 身份验证。默认为 no。要启用此机制，必须在此处和客户端相应的配置文件中都将此关键字设置为 yes。有关此机制的详细讨论，请参见第 260 页的 TrustedHostAuthentication。 |
| RhostsRSAAuthentication | 如果为 yes（默认值），则允许 Rhosts 和 RSA 身份验证。要启用此机制，必须在此处和客户端相应的配置文件中都将此关键字设置为 yes。有关此机制的详细讨论，请参见第 260 页的 Rhosts 和 RSA 身份验证。 |
| RSAAuthentication | 如果为 yes（默认值），则允许 RSA 身份验证。要启用此机制，必须在此处和客户端相应的配置文件中都将此关键字设置为 yes。有关此机制的详细讨论，请参见第 261 页的 RSA 身份验证。 |
| ServerKeyBits | 设置服务器密钥的位数。默认为 768。如果设置了 -b 命令行选项，则此值将被覆盖。 |
| SilentDeny | 如果为 yes，则向客户端抑制错误消息并在服务器上抑制日志记录。默认为 no。 |
| StrictModes | 如果为 yes（默认值），shhd 将不会授予那些主目录和/或 .root 文件由其他用户拥有或可被所有用户写入的用户的访问权限。 |
| Umask | 设置 sshd 及其子进程的 umask。必须使用带前导 0 的八进制数指定。默认情况下未设置。 |
| X11Forwarding | 如果为 yes（默认值），则允许 X Window System 转发。 |
| X11DisplayOffset | 指定可供 sshd 用于 X Window System 转发的第一个显示器编号。默认为 1。在其他 X Window System 应用程序存在的情况下，可能需要将其设置为更高的值。 |
| XAuthLocation | 指定 xauth 程序的路径。 |

示例 11-2 展示了一个 /etc/ssh/sshd_config 文件样本。我们将讨论以**粗体**显示的选项。其余部分很简单，可以在表 11.5 中找到。

### 示例 11-2 典型的 /etc/ssh/sshd_config 文件

```
# sshd config file
Port 22
ListenAddress 0.0.0.0
HostKey /etc/ssh/ssh_host_key
RandomSeed /etc/ssh/ssh_random_seed
ServerKeyBits 768
LoginGraceTime 600
KeyRegenerationInterval 3600
PermitRootLogin yes
IgnoreRhosts yes
StrictModes yes
QuietMode no
X11Forwarding yes
X11DisplayOffset 10
FacilitateLogging yes
PrintMotd yes
KeepAlive yes
SyslogFacility DAEMON
RhostAuthentication no
RhostRSAAuthentication yes
RSAAuthentication yes
PasswordAuthentication yes
AllowUsers mary paul bill
DenyHosts other *.evil.com
```

示例 11-2 中的 `ListenAddress 0.0.0.0` 项的效果是允许对系统中任何接口的 ssh 请求。您也可以指定单个地址，此时 sshd 将仅接受该地址上的请求。这对于具有多个接口但仅希望允许连接到其中一个接口的系统非常有用。您不能指定多个地址。

`IgnoreRhosts` *yes* 项将导致 sshd 忽略所有 `.rhosts` 和 `.shosts` 文件。但是请注意，此项不会导致 sshd 忽略 /etc/hosts.equiv。

`StrictModes` *yes* 项强制 sshd 忽略 `$HOME/.rhosts`、`$HOME/.shosts`、`$HOME/.ssh/authorized_keys` 和/或 `$HOME/.ssh/identity` 文件，如果这些文件由主目录中的用户以外的任何人拥有和/或可写。这将导致非密码身份验证失败。

`AllowUsers` mary paul bill 项将连接到此服务器的 sshd 限制为仅用户 mary、paul 和 bill。所有发起 ssh 请求的其他用户都将被拒绝。

`DenyHosts` other *.evil.com* 导致 sshd 拒绝来自主机 other 以及来自域名 evil.com 的任何主机的任何连接尝试。请注意，sshd 仅使用规范主机名，因此，例如，如果您先通过 /etc/hosts 然后通过 DNS 解析主机名，则需要指定其常规解析形式的主机名。在此，other 没有使用域名，因为它通过 /etc/hosts 解析，而 evil.com 是一个外部域名，始终通过 DNS 解析。

2. 主机名解析的控制是通过两个文件 /etc/host.conf 和 /etc/nsswitch.conf 进行的。

## 配置客户端

现在让我们描述 ssh 客户端程序的命令行参数及其配置文件。ssh 命令采用以下语法：

```
ssh [flags] hostname [command]
```

其中可选标志如表 11.6 中所述，hostname 是远程服务器的主机名或 IP 地址，并且可选地可以指定一个命令。

当调用 ssh 时，它首先从命令行获取配置信息，然后从用户的 $HOME/.ssh/config，最后从系统范围的 /etc/ssh/sshd_config。如果相同的参数设置不同，则第一个设置优先。表 11.6 记录了 ssh 的命令行选项。

表 11.7 列出了可以在 $HOME/.ssh/config 或 /etc/ssh_config 配置文件中指定的可用关键字或参数。这些文件中的所有空白行和以 # 开头的行都将被忽略。所有关键字均不区分大小写，关键字与其参数之间用空格或 = 分隔。除了特别注明的情况外，所有关键字都接受 yes 或 no 值。

## 表 11.6 ssh 的命令行选项

| 标志 | 描述 |
| :--- | :--- |
| -a | 禁用身份验证代理的转发。参见第 303 页的“禁用 X 和代理转发”。 |
| -c cipher | 指定对称密码。可用选项包括 idea、des、3des、blowfish、arcfour 和 none。美国版本的默认值是 blowfish；否则默认为 idea。none 选项会关闭加密，所有通过 ssh 传输的数据将是明文的。none 选项仅用于调试。 |
| -e escape | 为具有伪终端（pty）的会话设置转义字符。默认为 ~。将值设置为 none 会禁用转义。 |
| -f | 在身份验证和转发（如果有）之后将 ssh 放入后台。参见第 304 页的“探索 ssh 功能”中的示例。 |
| -g | 允许远程主机连接到本地转发的端口。这个危险选项在第 307 页的“端口转发和应用代理”中进行了讨论。 |
| -i file | 指定包含私钥的文件。默认情况下它保存在 $HOME/.ssh/identity 中。 |
| -l username | 指定在远程机器上登录的用户名。 |
| -n | 阻止从标准输入读取。此选项在第 304 页的“探索 ssh 功能”一节中进行了描述。 |
| -o option | option 可以替换为任何可以放入 ssh 配置文件中的 keyword=value。您必须在每个 keyword=value 前加上 -o 标志。 |
| -p port | 指定远程端口号；默认为 22。 |
| -q | 安静模式。抑制除致命错误消息以外的所有消息。 |
| -P | 指定使用非特权本地端口。使用此选项将禁用 Rhosts 身份验证和 Rhosts 和 RSA 身份验证。通常用于连接不允许使用特权源端口的系统。 |
| -t | 强制分配伪终端。适用于运行 curses 或其他基于屏幕的应用程序。 |
| -v | 详细模式。对于调试 ssh 的各个方面非常有用。可以通过运行 sshd -a 同时生成额外的调试信息（参见第 269 页的表 11.4）。 |
| -V | 打印版本号并退出。 |
| -x | 禁用 X Window System 转发。 |

