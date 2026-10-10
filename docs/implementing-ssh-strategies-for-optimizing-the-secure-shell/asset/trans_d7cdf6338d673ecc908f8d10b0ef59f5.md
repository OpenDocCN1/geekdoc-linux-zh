

### SSH 客户端命令行选项

- `+g`: 不转发端口。
- `+C`: 启用压缩。
- `-C`: 禁用压缩。
- `-4`: 使用 IPv4 进行连接。
- `-6`: 使用 IPv6 进行连接。
- `-o`: `option` 像从配置文件中读取该选项一样进行处理。
- `-l[tt]`: 选择 sshl-protocol 回退类型。
- `-h`: 显示此帮助信息。

如前所述，SSH 帮助文件内容详尽，展示了 SSH 可以提供的各种选项。从最基本的意义上讲，SSH 可以连接正在默认端口 22 上监听的 SSH 服务器。如果需要指定 22 以外的端口，必须使用 `-p` 开关；然而，如果不使用 `-p`，则默认使用端口 22。类似地，如果需要指定用户名，必须使用 `-l` 开关。如果不使用 `-l` 开关，将使用执行该命令的当前用户：

```
ssh 10.0.0.3 -l cdwivedi -p 22
cdwivedi's password:
Authentication successful.
Last login: Thurs June 12 05:52:06 2003 from 172.16.11.17
```

作为替代方案，可以使用 SSH 默认设置，而不使用任何开关编写相同的命令：

```
ssh cdwivedi@10.0.0.3:22
```

`-l` 和 `-p` 是 SSH 客户端使用的众多开关中的两个。接下来的部分将介绍本书其余部分中常用的一些重要开关。

第一个开关是 `-i`。`-i` 开关可用于指向用于向 SSH 服务器进行身份验证的公钥文件。公钥文件需要存在于 SSH 服务器上以便进行公钥身份验证，第 4 章将进一步讨论此问题。以下是 `-i` 开关的一个示例：

```
ssh 10.0.0.3 -i cdwivedi -p 60599 -i publickey.pub
```

`-L` 和 `-R` 开关分别用于本地端口转发和远程端口转发。第 6 章将讨论端口转发；但当前需要对语法有一般性的了解。本地端口转发允许通过 SSH 服务器将本地对某个端口的连接转发到远程服务器上的任意远程端口。例如，IP 地址为 10.0.0.100 且监听端口 143 的邮件服务器可以通过 SSH 进行访问。IP 地址为 10.0.0.3 的 SSH 服务器需要有一条到该机器路由。以下是使用 `-L` 开关进行本地端口转发的示例：

```
ssh 10.0.0.3 -l cdwivedi -L 143:10.0.0.100:143
```

也可以进行远程端口转发；第 6 章将进一步讨论。以下是远程端口转发的示例：

```
ssh 10.0.0.3 -l cdwivedi -R 139:127.0.0.1:139
```

还可以设置所需加密类型以及 MAC 算法类型。例如，如果 SSH 服务器仅接受使用三重 DES (3DES) 的连接，则应使用 `-c` 开关。3DES 是一种可用于加密数据的算法。这使得 3DES 能够用于加密遍历网络的数据。如果支持多种加密类型，可以使用多个 `-c` 选项。以下是两个加密选项的示例：

```
ssh 10.0.0.3 -l cdwivedi -c 3DES
ssh 10.0.0.3 -l cdwivedi -c 3DES -c Blowfish
```

使用的 MAC 算法可以是 MD5 或 SHA1。MD5 和 SHA1 都是可用于验证数据完整性的算法。MD5 使用源自数据输入的 128 位消息摘要，该摘要对数据是唯一的。SHA1 使用源自数据输入的 160 位消息摘要，该摘要同样对数据是唯一的。这使得 MD5 和 SHA1 哈希值可以用作特定数据块的指纹。为了使用 MAC 算法，应使用特定的选项（`hmac-md5` 或 `hmac-sha1`）配合 `-m` 标志，以对两个实体之间传输的数据进行哈希处理。以下是两个 MAC 选项的示例：

```
ssh 10.0.0.3 -l cdwivedi -m hmac-md5
ssh 10.0.0.3 -l cdwivedi -m hmac-sha1
```

`-f` 开关用于指向 SSH 会话的不同配置文件。每个 SSH 会话在尝试建立连接时都会使用配置文件作为输入。配置文件将在下一节“SSH 客户端配置文件”中进行讨论。如果终端用户需要连接两个或更多具有不同参数（例如监听不同端口）的 SSH 服务器，那么指向不同的配置文件比记忆 SSH 服务器所需的输入参数要容易得多。假设 SSH 服务器 A 监听端口 101，启用指向邮件服务器的本地转发，并要求使用 3DES 进行加密。此外，服务器 B 监听端口 701，启用指向文件服务器的本地转发，并要求使用 Blowfish 进行加密。如果不使用配置文件，这两条命令如下所示：

```
ssh 10.0.0.3 -l cdwivedi -p 101 -L 143:172.16.1.100:143 -c 3DES
ssh 10.0.0.4 -l cdwivedi -p 701 -L 139:172.16.1.200:139 -c Blowfish
```

虽然记住两条命令可能不难，但连接两个以上具有不同转发规则、不同端口规格和不同加密算法的 SSH 服务器将变得繁琐。使用两个配置文件可以显著简化登录过程和用户体验，如下面的示例所示：

```
ssh 10.0.0.3 -l cdwivedi -F mail.config
ssh 10.0.0.4 -l cdwivedi -F file.config
```

接下来的两个开关在使用 IPv4 或 IPv6 时非常简单。使用 IPv6 假定正在使用 IPv6 网络，这超出了本书和 SSH 的范围；然而，SSH 提供对 IPv6 数据报的支持。IPv4 是默认的数据报类型，但如果网络可用，可以使用这两个标志。以下是这两个开关的两个示例：

```
ssh 10.0.0.3 -l cdwivedi -4
ssh 10.0.0.3 -l cdwivedi -6
```

接下来的开关不会为 SSH 客户端增加功能，但确实提供了收集有关连接的额外信息的机会。`-d` 开关设置连接的调试级别。调试值越高，屏幕上打印的关于连接的信息就越多。以下是 `-d` 开关的一个示例。请注意密码请求之前出现的所有信息：

```
ssh 10.0.0.3 -l cdwivedi -d 1
debug: Connecting to 10.0.0.3, port 22...
debug: (SOCKS not used)
debug: client supports 3 auth methods: 'publickey,keyboard-interactive,password'
debug: Ssh2Common/sshc/sshcommon.c:537/ssh_common_wrap:
local ip = 10.0.0.3, local port = 1077
debug: Ssh2Common/sshc/sshcommon.c:539/ssh_common_wrap:
remote ip = 10.0.0.3, remote port = 22
debug: Remote version: SSH-1.99-OpenSSH_3.4pl
debug: OpenSSH: Major: 3 Minor: 4 Revision: 0
debug: Remote host key found from database.
debug: server offers auth methods
publickey,password,keyboard-interactive' .
debug: SshConfig/sshconfig.c:2717/ssh2_parse_config_ext:
Unable to open /root/.ssh2/identification
debug: server offers auth methods
publickey,password,keyboard-interactive'.
debug: server offers auth methods
publickey,password,keyboard-interactive'.
cdwivedi's password:
```

下一个信息类开关 `-V` 显示远程 SSH 服务器的版本。当试图了解远程 SSH 服务器正在运行什么版本以进行补丁修复和安全目的时，这很有帮助。以下是 `-V` 开关的一个示例：

```
ssh 10.0.0.3 -V
ssh: SSH Secure Shell 3.2.3 (non-commercial version) on i686-pc-linux-gnu
```

这里讨论的最后一个信息类开关是 `-q`。从本质上说，它告诉 SSH 服务器保持安静，不向最终用户显示任何警告消息。如果使用 `-q` 开关，SSH 服务器将仅显示对用户密码的请求。以下是 `-q` 开关的一个示例：

```
ssh 10.0.0.3 -q
root's password:
```

## SSH 客户端配置文件

既然我已经介绍了可以与 SSH 客户端一起使用的开关，我将讨论配置文件本身。表 3.1 描述了根据操作系统和 SSH 客户端类型，配置文件可能所在的位置。SSH 客户端配置文件分为以下几类：

- 通用
- 网络
- 加密
- 用户公钥认证
- 隧道
- SSH1 兼容性
- 认证

接下来的段落将探讨这些类别中的每一个。

